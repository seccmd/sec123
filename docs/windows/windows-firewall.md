Windows 防火墙
===

这个快速参考备忘单提供了使用 Windows 防火墙 常用命令的使用清单

防火墙管理
--------

### Powershell 命令行
<!--rehype:wrap-class=row-span-1 col-span-3-->

action | 参数
:--- | :---
封堵远程地址   | `New-NetFirewallRule -DisplayName Rule100 -Direction Inbound -Action Block -RemoteAddress 10.10.10.0/24`   
封堵本地端口   | `New-NetFirewallRule -DisplayName Rule100 -Direction Inbound -Action Block -Protocol TCP -LocalPort 8080`  
查看防火墙规则 | `Get-NetFirewallRule -DisplayName Rule100` 
查看防火墙规则 | `Get-NetFirewallRule -DisplayName Rule100 \| Get-NetFirewallAddressFilter `
删除防火墙规则 | `Remove-NetFirewallRule -DisplayName Rule100 ` 
防火墙运行状态 | `Get-NetFirewallProfile \| Select-Object Name,Enabled`
开启防火墙     | `Set-NetFirewallProfile -Enabled True` 
关闭防火墙     | `Set-NetFirewallProfile -Enabled False`
<!--rehype:className=style-list-->


### CMD 命令行
<!--rehype:wrap-class=row-span-2 col-span-3-->

action | 参数
:--- | :---
封堵远程地址   | `netsh advfirewall firewall add rule name="Rule100" dir=in action=block remoteip=10.10.10.0/24`
封堵本地端口   | `netsh advfirewall firewall add rule name="Rule100" dir=in action=block protocol=TCP localport=8080`
查看防火墙规则 | `netsh advfirewall firewall show rule name="Rule100" `
删除防火墙规则 | `netsh advfirewall firewall delete rule name="Rule100" `
防火墙运行状态 | `netsh advfirewall show currentprofile`
开启防火墙     | `netsh advfirewall set allprofiles state on`
关闭防火墙     | `netsh advfirewall set allprofiles state off`
关闭防火墙     | `net stop sharedaccess    `
<!--rehype:className=style-list-->

