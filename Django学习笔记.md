# Django学习笔记
这里记录Django框架的学习心得，以免以后忘记了。

## 安装Python3
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
## 安装Django
```Shell
pip install Django
```

## 创建项目
```Shell
django-admin startproject mysite
```

## 部署项目
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
```	INI
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
	/home/kevin/.local/bin/uwsgi --ini /etc/uwsgi/apps-enabled/DjangoTutorial.ini &
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