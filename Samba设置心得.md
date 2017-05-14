# Samba File Server
## 建立共享目录并设置权限
这里考虑用`Sticky Bit`

```
sudo mkdir -p /path/to/dir
sudo chmod 1777 /path/to/dir
```

## 配置Samba
- `[global]`里面保持默认即可
- `[homes]`注释打开，`browsable = no`
- 添加自己的目录`[my_share]`
	- `path = /path/to/share`
	- `browsable = yes`
	- `guest ok = yes`
	- `read only = yes`
	- `write list = user`
	- `force create mode = 755`
	- `force directory mode = 0755`