# 配置
- cache-size-mb: 设置缓存大小(e.g. 16)
- download-dir: 已下载目录
- incomplete-dir: 下载中的临时目录
- watch-dir: 监听种子目录
- preallocation： 预分配模式(e.g. 2 全分配)
- rpc-host-whitelist: 远程访问域名白名单(e.g. *.qingling.org)
- rpc-whitelist: 远程访问IP白名单(e.g. 127.0.0.1,172.168.*.*)
- umask: 权限控制(e.g. 2)

# 种子制作
`transmission-create -p -t TRACKER -o FILENAME.torrent <file|directory>`
