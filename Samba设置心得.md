# Samba File Server
## 建立共享目录并设置权限
这里考虑用`Sticky Bit`

```
sudo mkdir -p /path/to/dir
sudo chmod 1777 /path/to/dir
```

## 建立用户
```bash
cut -d: -f1 /etc/passwd		// 列出所有用户
adduser new_user				// 添加用户
userdel -r old_user			// 删除用户并删除home目录
passwd username				// 更改密码
chsh username					// 更改Shell

cut -d: -f1 /etc/group		// 列出所有组
usermod -g GROUP username	// 更改用户的组
```

## 将用户添加到Samba
```bash
smbpasswd -a username
```

## 配置Samba
- `[global]`里面保持默认即可
- 添加自己的目录`[my_share]`
	- `path = /path/to/share`
	- `browseable = yes`
	- `guest ok = yes`
	- `read only = yes`
	- `write list = @users`
	- `force create mode = 755`
	- `force directory mode = 0755`

## 重启Samba
```bash
systemctl restart smbd.service nmbd.service
```

## 解决GROUP没有写权限的问题
编辑`/etc/login.defs`，将`UMASK	`设置为`002`

## 光驱
```
[cdrom]
    comment = qlserver cdrom
    path = /mnt/cdrom
    guest ok = yes
    read only = yes
    browseable = yes
    root preexec = /bin/mount -t auto /dev/cdrom /mnt/cdrom
    root postexec = /bin/umount /mnt/cdrom
```

## `mount`远端Samba目录到本机
`mount -t cifs -o user=xxx //IP/path/to/folder /mnt/point`

## 解决SELinux只能看到目录却看不到文件的问题
```
chcon -Rt samba_share_t /path/to/share
```

## 其他注意事项
- 不要把要共享的目录放在`/root`下面
