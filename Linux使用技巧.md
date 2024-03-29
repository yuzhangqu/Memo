# 有用的Linux命令
- `init 3` 切换到文本模式
- `init 5` 切换到图形模式
- `runlevel` 查看最近两次的运行模式
- `id -u` 查看当前帐号的uid
- `tty` 查看当前终端
- `lsb_release -a` 查看操作系统版本
- `uname -r` 查看内核版本
- `hostname` 查看主机名
- `lsblk/lscpu` 查看磁盘/CPU信息
- `type` 查看命令类型
- `hash` 查看命令缓存
- `alias/unalias` 设置/取消别名
- `enable` 设置命令有效性
- `which/whereis` 定位命令
- `who/whoami/who am i/w` 查看用户登录信息
- `date` 系统日期
- `hwclock` 硬件时钟
- `cal` 日历
- `screen` screen会话命令
- `hexdump` 查看文件
- `iconv` 文件编码转换
- `whatis` 查看命令简短描述
- `man CHAPTER COMMAND` 查看命令的指定章节
- `info COMMAND` 类似网站的帮助
- `history` 查看历史命令,-c清空
- `!!/!:0` 执行上一条命令/执行上一条命令不带参数
- `!STRING` 重复前一个以STRING开头的命令
- `!$:p/!*:p` 打印上一条命令的最后一个参数/所有参数
- `!:gs/S1/S2` 将上一条命令的S1替换为S2执行
- `rm -- -a` 删除以`-`开头的文件
- `basename/dirname` 取出路径的基名和目录名
- `stat` 查看文件或文件系统的状态信息
- `file` 分析文件类型
- `>、2>、&>、2>&1`STDOUT、STDERR、所有输出重定向、STDERR重定向到STDOUT
- `tr` 从字符集合1映射到集合2, `tr -d` 删除字符集合1中的字符, `-c`选项用字符集合1的补集, `-s`去重(`-dc`、`-sc`搭配使用效果不错)
- `tee` 多重重定向
- `locate/updatedb` 搜索文件/更新搜索索引数据库
- `find [OPTION]... [搜索路径] [搜索条件] [处理动作]` 实时查找工具, `-name`按文件名, `-type`按文件类型
- `chfn/chsh/chage` 更改用户信息/更改用户SHELL/更改用户有效期信息
- `getent database key` 获取database里面主键为key的一行
- `groupmems -a USERNAME -g GROUPNAME` 将用户加到组里
- `newgrp GROUPNAME` 登陆到新的组作为主组
- `passwd/gpasswd` 更改用户/组的密码
- `vipw/vigr/pwck/grpck` 编辑`pwsswd`文件/编辑`group`文件/检查`pwsswd`文件/检查`group`文件
- `useradd/usermod/userdel` 用户管理命令
- `groupadd/groupmod/groupdel` 组管理命令
- `su [-] USERNAME -c 'COMMAND'` 切换用户
- `chown/chgrp/chmod` 更改所有者/组/权限
- `chattr +i/chattr +a/lsattr` 增加`immutable`属性/文件只能追加/列出扩展属性
- `getfacl/setfacl -m ACL/setfacl -x ACL/setfacl -k/setfacl -b` 获取/修改/删除/清除默认/清空文件的ACL权限(ACL形如`[d]:u/g:USERNAME:rwx`)
- `getfacl file1 | setfacl --set-file=- file2` 复制file1的ACL权限到file2
- `ss -tn` 显示并发连接
- `binwalk -D 'png image:png' file1` 从file1里面解出隐藏的png图片

# 系统变量
- `$SHELL` 当前的shell
- `PS1` 命令提示符格式
- `$LANG` 系统语言,保存在`/etc/locale.conf`文件中,可通过`localectl set-locale LANG=XXX`修改
- `$HISTSIZE` 历史命令缓存大小,可在`/etc/profile`中修改
- `$PWD/$OLDPWD` 当前目录/上次目录

# Tips
- uid为0、提示符为`#`是超级用户，uid非0、提示符为`$`是普通用户
- 物理终端console，虚拟终端tty，伪终端pty（例如:ssh远程连接）
- `/etc/shells`中存储了支持的shell
- 开机自动运行的程序用的是shell是nologin
- `/etc/profile.d/`目录下存放启动执行脚本
- 命令解析顺序:alias -> 内部命令 -> Hash表 -> $PATH中搜索 -> 找不到
- `~/.bashrc`是用户的别名等配置,`/etc/bashrc`是全局的
- `\COMMAND` 绕过别名执行原命令
- ASCII码一共规定了128个字符的编码,占用一个字节的后7位
- Unicode编码方案有:UTF-8(1-4个字节)、UTF-16(2-4个字节)、UTF-32(4个字节).对于需要大于1个字节来表示的字符,第一个字符的前N位设为1,N+1位设为0,剩余N-1个字节的前两位设为10.再用内容填充.
- `{}`可以用来扩展,`file{1,3,5}`扩展为file1、file3、file5
- `~/.bash_history`存放历史命令
- `Ctrl + r`搜索历史, `Ctrl + g`退出搜索模式
- `!$`用上一个命令的最后一个参数, `ESC .`、`Alt + .`同样可以调出
- `/etc/motd`是登陆后显示内容,`/etc/issue`是登陆前显示内容
- `Ctrl + a`光标移到命令行首,`Ctrl + e`移到行尾
- `Ctrl + u`删除到行首,`Ctrl + k`删除到行尾,`Alt + r`删除整行
- `www.pathname.com/fhs`里面有目标的存放标准
- Linux下的文件类型:`-`普通文件,`d`目录文件,`b`块设备,`c`字符设备,`l`符号链接文件,`p`管道文件,`s`套接字文件
- 在`/misc`目录下进入隐藏的`cd`子目录,即可访问光盘的信息
- `atime`读取时间,`mtime`内容修改的时间,`ctime`元数据修改的时间
- `~-`前一个工作目录,`^`在通配符中表示排除
- `man 7 glob`可查看预定义的通配符
- `cp -a`可以保留文件各种属性
- 软链接 vs 硬链接：同一个文件？跨分区？链接数增加？原始文件删除，链接可访问？文件大小？支持目录？相对的路径？
- `set -C/+C`禁止/允许文件覆盖
- `cat > f1 << EOF` 多行重定向
- `|&`标准输出和错误输出都通过管道, 管道中的`-`用来当做临时文件(`tar -cvf - /home | tar -xvf -`)
- `/etc/passwd、/etc/group、/etc/shadow、/etc/gshadow` 用户信息、组信息、用户密码(密码前的`!`表示禁用)、组密码
- 启动菜单按`e`进入，找到`linux16`那行，添加`init=/bin/bash`，按`ctrl+x`启动。运行`mount -o rw,remount /`开启读写
- `/etc/default/useradd、/etc/skel/*、/etc/login.defs`是新建用户相关的文件，`newusers/chpasswd`批量新建用户/修改用户口令
- `umask` 通过掩码形式生成默认权限(文件用`666`减, 文件夹用`777`减)
- `SUID` 在所有者的执行权限位置,`s`在二进制文件上可在运行时拥有程序所有者的权限。通过`chmod u+s`或`chmod 4777`添加
- `SGID` 在所属组的执行权限位置,`s`在二进制文件上可在运行时拥有程序所属组的权限,`s`在目录上可使该目录下创建的文件都是该目录的组。通过`chmod g+s`或`chmod 2777`添加
- `Sticky` 在其他人的执行权限位置,`t`在目录上只有文件的所有者和`root`才能删除该目录下的文件。通过`chmod o+t`或`chmod 1777`添加
- 设置了ACL权限之后，传统的组权限移到ACL里面，取而代之的是`mask`权限。`mask`是用户、组的最大权限，可通过`setfacl -m mask::rwx/chmod g=rwx`来设置

# 文本处理
- `cat`：显示文件内容
    - `-E`：显示换行符
    - `-A`：显示所有控制符
    - `-n`：显示所有行号
    - `-b`：显示非空行行号
    - `-s`：压缩连续的空行成一行
- `tac`：从后往前显示文件内容
- `rev`：文件每行字符级反转
- `more/less`：分页显示
- `head/tail`：显示开始/末尾10行
    - `-n`：指定显示行数(`head -n -NUM`可以排除末尾NUM行, `tail -n +NUM`可以从第NUM行开始)
    - `-c`：指定显示字符数
    - `-f/-F`：跟踪文件/带重试跟踪文件(仅tail有效)
- `cut`：取出每一行的指定部分
    - `-dDELIM`：指定`DELIM`取代Tab成为分隔符
    - `-bLIST`：选取指定的BYTE(`LIST`可以用`,`分隔或者`-`范围)
    - `-cLIST`：选取指定的字符
    - `-fLIST`：选取指定的域
    - `--output-delimiter`：指定输出的分隔符
- `paste`：按行合并多个文件
    - `-d`：指定显示分隔符
    - `-s`：每行合并一个文件的各个行
- `wc`：统计行数、单词数、字节数
    - `-l`：只显示行数
    - `-w`：只显示单词数
    - `-m`：只显示字符数
    - `-c`：只显示字节数
    - `-L`：显示最长的行的长度
- `sort`：排序
    - `-tSEP`：使用`SEP`作为字段界定符
    - `-kKEYDEF`：使用第`KEYDEF`个字段作为排序主键
    - `-r`：逆向排序
    - `-R`：随机排序
    - `-n`：数字排序
    - `-f`：忽略大小写
    - `-u`：输出去重
- `uniq`：从输出中删除相邻的重复行
    - `-d`：仅显示重复过的行
    - `-u`：仅显示未重复过的行
    - `-c`：显示每行重复出现次数
- `diff`：按行比较文件内容
    - `-u`：显示统一格式信息(可用于`patch`)
- `patch`：打补丁
    - `-b`：备份即将被打补丁的文件
- `grep`：文本过滤
    - `-v`：显示不匹配的行
    - `-i`：忽略大小写
    - `-n`：显示行号
    - `-c`：显示匹配到多少行
    - `-o`：仅显示匹配到的字符串
    - `-A/B/CNUM`：额外显示前`NUM`行/后`NUM`行/前后`NUM`行
    - `-e`：使用多次实现`OR`的效果
    - `-w`：全词匹配
    - `-f`：使用模式文件，匹配其中的关键字(可使用两个文件取交集`grep -f FILE1 FILE2`)
- `sed`：
- `awk`：

# 扩展正则表达式
- 字符匹配
    - `.`：匹配任意单个字符
    - `[]`：匹配指定范围内的任意单个字符
    - `[^]`：匹配指定范围外的任意单个字符
    - `[:alnum:]`：字母和数字
    - `[:alpha:]`：字母
    - `[:lower:]`：小写字母
    - `[:upper:]`：大写字母
    - `[:blank:]`：空白字符
    - `[:space:]`：水平和垂直的空白字符(比`[:blank:]`的范围广)
    - `[:cntrl:]`：控制字符
    - `[:digit:]`：十进制数字, `[:xdigit:]`为十六进制数字
    - `[:graph:]`：可打印的非空白字符
    - `[:print:]`：可打印的字符
    - `[:punct:]`：标点符号
- 匹配次数
    - `*`：任意次数
    - `?`：前面的字符0次或1次
    - `+`：前面的字符至少1次
    - `{n}`：前面的字符n次
    - `{m,n}`：前面的字符出现m次到n次(m省略代表下限0, n省略代表上限无穷大)
- 位置锚定
    - `^`：行首锚定
    - `$`：行尾锚定
    - `\<`：词首锚定(也可用`\b`)
    - `\>`：词尾锚定(也可用`\b`)
- 分组
    - `()`：将一个或多个字符捆绑在一起当做整体处理
    - `\k`：表示第k对括号匹配到的字符(非模式本身)
- 或者
    - `|`：或者关系
- 示例
    - IP地址：`(([1-9]?[0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\.){3}([1-9]?[0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])`

# 终端
- 代理
    - `export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890`
