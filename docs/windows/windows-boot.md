Windows 开机启动
===

在操作系统中，分析查看开机启动信息。
典型场景：在应急响应过程中，排查可疑系统启动项，应即时禁用或者删除恶意系统启动项。
注意事项：需要联系系统管理员确认启动项是否合法，防止错误禁用和删除了正常的合法启动项。

查看开机启动项
--------

### Powershell 命令行
<!--rehype:wrap-class=row-span-2 col-span-3-->

参数 | action
:--- | :---
`Get-CimInstance Win32_StartupCommand \| Select-Object Name, command, Location, User \| Format-List`   | 查看开机启动项
<!--rehype:className=style-list-->

``` powershell
# 查看开机启动项
Get-psdrive
cd HKLM:\
Set-location -path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion
Get-childitem -ErrorAction SilentlyContinue \| Where-Object {$_.Name -like "*Run*"}
Set-location -path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\
Get-childitem -ErrorAction SilentlyContinue \| Where-Object {$_.Name -like "*Run*"}
```

查看开机启动项
--------

### CMD 命令行
<!--rehype:wrap-class=row-span-2 col-span-3-->

参数 | action
:--- | :---
`reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`   | 查看开机启动项
`reg query HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`   | 查看开机启动项
<!--rehype:className=style-list-->

### WMIC 命令行
<!--rehype:wrap-class=row-span-2 col-span-3-->

参数 | action
:--- | :---
`wmic startup get caption,command`   | WMIC 查看开机启动项
<!--rehype:className=style-list-->
