Windows 进程与任务管理
===

这个快速参考备忘单提供了使用 Windows 进程与任务 常用命令的使用清单

进程管理
--------

### Powershell 命令行

参数 | action
:--- | :---
`Get-Process`   | 查看进程
`Start-Process`   | 启动进程
`Stop-Process -Force -ID <PID>`   | 关闭进程
`wmic process get name,processid` | WMIC 查看进程

### tasklist 命令
<!--rehype:wrap-class=col-span-1-->

参数 | action
:--- | :---
`taskmgr.exe`   | 任务管理器
`tasklist`   | 查看进程
`tasklist /V /FO CSV`   | 查看进程详情
`tasklist /SVC /FO LIST`   | 查看服务



### taskkill 命令
<!--rehype:wrap-class=col-span-1-->

参数 | action
:--- | :---
`taskkill /f /pid <PID>`   | 终止指定PID进程 
`taskkill /IM notepad.exe`   | 终止指定进程名
`taskkill /PID 1230 /PID 1241 /T` | 终止多个PID进程 
`taskkill /F /IM cmd.exe /T` | 强制终止进程名


服务管理
--------

### Powershell 命令行

参数 | action
:--- | :---
`Get-Service`   | 查看系统服务
`New-Service`   | 新建系统服务
`Start-Service -Name <SERVICE_NAME>`  | 启动系统服务 
`Stop-Service -Name <SERVICE_NAME>`   | 关闭系统服务

### sc 命令
<!--rehype:wrap-class=col-span-1-->

参数 | action
:--- | :---
`sc query`   | 查看全部服务
`sc query eventlog` | 显示服务的状态
`sc start` | 启动服务
`sc stop`  | 停止服务
`sc create` | 创建服务
`sc delete` | 删除服务


### CMD 命令
<!--rehype:wrap-class=col-span-1-->

参数 | action
:--- | :---
`services.msc`   | 服务控制台
`net start ` | 查看服务
`net start <SERVICE_NAME>` | 启动服务
`net stop <SERVICE_NAME>`   | 关闭服务



计划任务
--------

### Powershell 命令行

参数 | action
:--- | :---
查看计划任务     | `Get-ScheduledTask \| Format-Table -AutoSize`
查看指定计划任务 | `Get-ScheduledTask -TaskName Office* \| Format-Table -AutoSize`
禁用计划任务     | `Disable-ScheduledTask -taskname "Adobe Flash Player Updater"`
启用计划任务     | `Enable-ScheduledTask -taskname "Adobe Flash Player Updater"`
<!--rehype:className=style-list-->

### schtasks 命令

参数 | action
:--- | :---
显示所有计划任务     | `schtasks.exe /Query `
中止当前正在运行的计划任务 | `schtasks.exe /End /TN \Microsoft\Windows\NlaSvc\WiFiTask`
删除计划任务     | `schtasks.exe /Delete /F /TN \Microsoft\Windows\NlaSvc\WiFiTask`
<!--rehype:className=style-list-->

### CMD 命令行

参数 | action
:--- | :---
`taskschd.msc`     | 显示所有计划任务

开机启动项
--------

### Powershell 命令行
<!--rehype:wrap-class=row-span-1 col-span-2-->

参数 | action
:--- | :---
`Get-CimInstance Win32_StartupCommand \| Select-Object Name, command, Location, User \| Format-List`   | 查看开机启动项
<!--rehype:className=style-list-->

``` powershell
# 注册表查看开机启动项
Get-psdrive ; cd HKLM:\
Set-location -path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion
Get-childitem -ErrorAction SilentlyContinue \| Where-Object {$_.Name -like "*Run*"}
Set-location -path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\
Get-childitem -ErrorAction SilentlyContinue \| Where-Object {$_.Name -like "*Run*"}
```

### CMD 命令行

#### 查看开机启动项

```cmd
reg query ^
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

reg query ^
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

wmic startup get caption,command
```


