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

# 系统变量
- `$SHELL` 当前的shell
- `PS1` 命令提示符格式
- `$LANG` 系统语言,保存在`/etc/locale.conf`文件中,可通过`localectl set-locale LANG=XXX`修改
- `	$HISTSIZE` 历史命令缓存大小,可在`/etc/profile`中修改

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