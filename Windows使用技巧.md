# Windows 7 & Windows 8局域网共享
1. 确保在同一局域网内
2. 计算机名不重复
3. 工作组名一样
4. 要共享的电脑设置了开机密码
5. Windows启用Guest账户
6. Windows更改高级共享设置，关闭密码保护共享

# Windows CMD设置代理
```
netsh winhttp set proxy IP:PORT
netsh winhttp reset proxy
```

# 安装SSH服务端
```
// 检查OpenSSH安装情况
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

// 安装OpenSSH服务端
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

// 启动sshd服务
Start-Service sshd

// 检查sshd服务状态
Get-Service sshd

// 设置sshd服务开机启动
Set-Service -Name sshd -StartupType 'Automatic'

// 设置ssh的默认shell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe"  -PropertyType String -Force
```
