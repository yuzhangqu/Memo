# Django学习笔记
这里记录Django框架的学习心得，以免以后忘记了。

## 配置环境
### 安装Python3
Django是`python`框架，`python`肯定是要有的。虽然`Mac`自带`python 2.7`，但是作为一个刚刚入行的新手，完全应该顺应时代的召唤，安装最新版的`python`(我当时装的是`3.6.1`版本)。

```Shell
sudo apt-get install python3
```

安装好之后，有了`python3`和`pip3`，使用起来不是很方便。这要用到`python 3.6`自带的`venv`模块。

```Shell
python3 -m venv /path/to/new/virtual/environment
```

激活虚拟环境之后，`python`和`pip`就是带`3`的版本了。

```Shell
source /path/to/new/virtual/environment／bin/activate  // 激活
deactivate  // 去激活
```

### 安装Django
```Shell
pip install Django
```

## 项目构建
### 创建项目
```Shell
django-admin startproject mysite .
```

### 创建应用
```
python manage.py startapp user
```

### 注册应用
```
INSTALLED_APPS = [
    ...,
    'user',
]
```

### 新增模型Model
- 字段类
    - AutoField：自增整数字段
    - BooleanField：布尔值字段（对应控件CheckboxInput）
    - NullBooleanField：True、False、null
    - CharField：字符串字段（对应控件TextInput）
    - TextField：大文本字段（对应控件TextArea）
    - IntegerField：整数字段
    - BigIntegerField：大整数字段，8字节
    - DecimalField
    - FloatField
    - DateField：使用datetime.date实例，对应控件TextInput，关联一个JS编写的日历控件
    - DateTimeField：使用datatime.datetime
    - FileField
    - ImageField
- 关系类型字段类
    - ForeignKey：外键，表示一对多
    - ManyToManyField：多对多
    - OneToOneField：一对一
- 字段选项
    - db_column：字段名字，不指定则跟属性名相同
    - primary_key：是否主键，默认为False
    - unique：是否唯一键，默认为False
    - default：新对象产生的时候填入的缺省值
    - null：是否可为null，默认为False
    - blank：Django表单验证中，是否可以不填写，默认为False
    - db_index：字段是否有索引，默认为False
- 模型定义
```python
class XXX(models.Model):
    class Meta:
        db_table = '表名'
    字段名 = models.XXXField(kwargs)
```

### 注册模型
```python
from .models import XXX
admin.site.register(XXX)
```

### 路由
- Function views
    1. Add an import: from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
- Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
- Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
- path() always matches the complete path(omit `^` and `$`)
- path converter
```
# path converters can convert parameters to the appropriate type
path('posts/<int:post_id>/', post_detail_view)
```
- built-in converters
    1. str: Equivalent to `[^/]+`, Returns a string (str).
    2. int: Equivalent to `[0-9]+`, Returns an integer (int).
    3. slug: Equivalent to `[-a-zA-Z0-9_]+`, Returns a string (str).
    4. uuid: Example: `075194d3-6885-417e-a8a8-6c931e272f00`, Returns a UUID instance (uuid.UUID).
    5. path: Equivalent to `.+`, Returns a string (str).

### 创建视图
```python
from django.http import HttpResponse, JsonResponse
def xxx_view(request, post_id):
    return JsonResponse({'id':post_id})
```

### 使用模板
```python
from django.shortcuts import render
def xxx_view(request, post_id):
    return render(request, 'post.html', {'id':post_id})
```
- 模板语法
    1. 变量
        - `{{ variable }}`
        - 如果写成`{{ foo.bar }}`的形式，先尝试字典查找，再尝试属性或方法查找，再尝试数字索引查找
    2. 模板标签
        - if/else标签：条件支持and、or、not
        ```
        {% if condition1 %}
            ...
        {% elif condition2 %}
            ...
        {% else %}
            ...
        {% endif %}
        ```
        - for标签：给标签增加一个`reversed`可反向迭代，forloop.counter/counter0/revcounter/revcounter0/first/last/parentloop
        ```
        <ul>
        {% for person in person_list %}
            <li>{{ person.name }}</li>
        {% endfor %}
        </ul>
        ```
        - `{% csrf_token %}`：防止跨站攻击
    3. 注释标签
        - 单行注释：`{# XXX #}`
        - 多行注释：`{% comment %} XXX {% endcomment %}`
    4. 过滤器
        - `{{ 变量|过滤器 }}`
        - first：取列表第一个元素
        - last：取列表最后一个元素
        - yesno：翻译True、False、None。`{{ value | yesno:"yeah,no,maybe" }}`
        - add：加法`{{ value | add:"-100"}}`，列表合并`{{ mylist | add:otherlist }}`
        - divisibleby：能否被整除`{{ value | divisibleby:"3" }}`
        - addslashes：加反斜杠
        - length：返回变量长度
        - default：如果等效None则使用缺省值。`{{ value | default:"nothing" }}`
        - default_if_none：如果是None则使用缺省值
        - date：按格式字符串格式化date或datetime对象。`{{ pub_date | date:"n j, Y" }}`
        ```
        <ul>
        {% for id in ids %}
            <li style='color:{{ forloop.counter|divisibleby:"2"|yesno:"#F00, #00F" }};'>{{ id }}</li>
        {% endfor %}
        </ul>
        ```

### 迁移文件
```
python manage.py makemigrations
python manage.py migrate
```

### 本地化
```python
# settings.py
LANGUAGE_CODE = 'zh-Hans'
USE_TZ = True
TIME_ZONE = 'Asia/Shanghai'
```

### 启动服务
```
python manage.py runserver
```

## 项目部署
目标是实现这样的结构：``the outside world <-> nginx <-> the socket <-> uwsgi``

### 准备工作
```Shell
#全局环境安装uwsgi和nginx
sudo pip3 install uwsgi
sudo apt-get install nginx
```

### 配置Nginx
```Nginx
upstream django {
    # 声明socket位置，这里要注意文件权限问题
    server unix:///tmp/uwsgi.sock;
}

server {
    listen      80;
    # 多个名字用空格分开
    server_name .qingling.org 172.168.1.1;
   charset     utf-8;

   client_max_body_size    75M;

   location /static/ {
       alias   /home/kevin/repos/DjangoTutorial/static/;
   }

   location / {
       uwsgi_pass  django;
       include     /etc/nginx/uwsgi_params;
   }
}
```

#### Nginx的常用指令
```
sudo /etc/init.d/nginx restart
cat /var/log/nginx/error.log
```

### 配置uwsgi
```INI
[uwsgi]

#The base directory
chdir           = /home/kevin/repos/DjangoTutorial/
module          = mysite.wsgi
home            = /home/kevin/myenv
chmod-socket    = 666

master          = true
processes       = 10
socket          = /tmp/uwsgi.sock
vacuum          = true
```

### 让uwsgi开机启动
1. 编辑`/lib/systemd/system/rc-local.service`文件，加入`[Install]`那一段：
```
[Unit]
Description=/etc/rc.local Compatibility
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes
GuessMainPID=no

[Install]
WantedBy=multi-user.target
```

2. 编辑`/etc/rc.local`文件，加入启动指令：
```Shell
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.
/home/kevin/.local/bin/uwsgi --touch-reload /tmp/reload.txt --ini /etc/uwsgi/apps-enabled/DjangoTutorial.ini &
exit 0
```

3. 启动`rc-local`
```
sudo chmod +x /etc/rc.local
sudo systemctl enable rc-local

#下面的是一些常用指令
sudo systemctl start rc-local
sudo systemctl status rc-local
```