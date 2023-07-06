Windows 工具脚本
===

这个快速参考备忘单提供了使用 Windows 工具脚本 常用命令的使用清单

工具
--------

### 安全工具

参数 | action
:--- | :---
[Microsoft Sysinternals](https://docs.microsoft.com/en-us/sysinternals/downloads/) |
[Process Hacker](http://processhacker.sourceforge.net) |
[AutoRuns](https://filehippo.com/zh/download_autoruns) |
[HuoRong 火绒 ](https://www.huorong.cn) |

### 常用工具
<!--rehype:wrap-class=col-span-2-->

参数 | action | item | item2 | item2
:--- | :--- | :--- | :--- | :---
[Chocolatey](https://chocolatey.org)        | [DeepL翻译](https://www.deepl.com/)                         | [IDM 下载](https://internetdownloadmanager.com/) | [KeePass]()
[Snipaste 截图](https://zh.snipaste.com)    | [科大翻译](https://fanyi.xfyun.cn/console/trans/doc)        | [FDM 下载](https://freedownloadmanager.org/)     | [Mybase]()
[Iridium 浏览器](https://iridiumbrowser.de) | [搜狗翻译](https://fanyi.sogou.com/document)                | [视频下载](https://youtube.iiilab.com/)          | [MobaXterm]()
[Start.me 导航](https://start.me)           | [福昕翻译](https://fanyi.pdf365.cn/doc)                     | [Tampermonkey](https://www.fkxz.cn/)             | [Notepad++]()
[永中 Office](https://www.yozosoft.com/)    | [知云文献](http://www.zhiyunwenxian.cn)                     | [Wireshark](https://www.wireshark.org)           | [Proxifier]()
[7zip 压缩](https://www.7-zip.org/)         | [沉浸翻译](https://immersive-translate.owenyoung.com/)      | [Fiddler](https://www.telerik.com)               | [VS Code]()


### JDK 下载

#### 国内 JDK 下载服务

地址：http://www.codebaoku.com/jdk/jdk-index.html

#### Oracle 共享账号

参数 | action
:--- | :---
`Chad1962@rhyta.com`   | KETQbd27NmhT9j8
`hoi@muellmail.com`    | Qwert1234
`erfede@yopmail.com`   | Bellapete!1
`b7293568@urhen.com`   | Y8l0W5KsDHB3YeNpn2y


### Win 安装 ssh 服务
<!--rehype:wrap-class=col-span-2-->

```powershell
# Search the OpenSSH
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
# Start the sshd service
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
```

### Python 环境

#### 安装

```
# Python 安装包
http://npm.taobao.org/mirrors/python/

# pip 国内镜像
pip3 install -i https://mirrors.aliyun.com/pypi/simple/ requests
```

#### 示例

```bash
$ python2 -m SimpleHTTPServer 8000
$ python3 -m http.server 8000

# 导入 requests 包
import requests

# 发送请求
x = requests.get('https://www.runoob.com/')

print(response.status_code)  # 获取响应状态码
print(response.headers)  # 获取响应头
print(response.content)  # 获取响应内容
print(x.text)            # 返回网页内容
```

### Golang 环境

#### 安装

```
# 下载Win安装包
https://studygolang.com/dl

# 更换国内源
set GO111MODULE=on 
set GOPROXY=https://mirrors.aliyun.com/goproxy
```

#### 示例

```bash
# main.go
package main
import (
    "fmt"
    "net/http"
)
func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Welcome to new server!")
    })
    http.ListenAndServe(":5050", nil)
}

$ go build -o httpserver main.go
```

### NodeJS 环境

#### 安装

```
# 下载Win安装包
https://nodejs.org/en/

# 国内镜像源 https://npmmirror.com/
npm config set registry https://registry.npm.taobao.org
```
#### 示例

```bash
$ npm install -g http-server
$ http-server C:\temp -p 8000

# Linux安装nodejs
wget https://nodejs.org/dist/v16.15.0/node-v16.15.0-linux-x64.tar.xz
tar -xJvf node-v16.15.0-linux-x64.tar.xz -C /usr/local/lib/nodejs 
vi ~/.profile 
  export PATH=//usr/local/lib/nodejs/node-v16.15.0-linux-x64/bin:$PATH
source ~/.profile
$ node -v 
$ npm version 
$ npx -v
```


脚本
--------

### Windows Initial System Examination
<!--rehype:wrap-class=col-span-3-->

```shell
# Look at event logs	
eventvwr

# Examine network configuration	
arp -a
netstat -nr

# List network connections and related details	
netstat -nao
netstat -vb
net session
net use

# List users and groups	
lusrmgr
net users
net localgroup administrators
net group administrators

# Look at scheduled jobs	
schtasks

# Look at auto-start programs	
msconfig

# List processes	
taskmgr
wmic process list full

# List services	
net start
tasklist /svc

# Check DNS settings and the hosts file	
ipconfig /all
more %SystemRoot%\System32\Drivers\etc\hosts
ipconfig /displaydns

# Verify integrity of OS files (affects lots of files!)	
sigverif

# Research recently-modified files (affects lots of files!)	
dir /a/o-d/p %SystemRoot%System32

# Avoid using Windows Explorer, as it modifies useful file system details; use command-line.
```

参考：[security-incident](https://zeltser.com/security-incident-survey-cheat-sheet/)


### Incident Response: Windows Cheatsheet
<!--rehype:wrap-class=col-span-3-->

```shell
# Check user accounts
lusrmgr.msc
net user
Get-LocalUser

#Check Administrators
net localgroup administrators
Get-LocalGroupMember Administrators

# Check processes
taskmgr.exe
tasklist
Get-Process
wmic process get name,parentprocessid,processid
wmic process where 'ProcessID=PID' get CommandLine

# Check Services
services.msc
net start
sc query | more
tasklist /svc
Get-Service | Format-Table -AutoSize

# Task Scheduler

## Administrative Tools (GUI)
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Administrative Tools
schtasks
taskmgr (Check Startup)
wmic startup get caption,command
Get-CimInstance Win32_StartupCommand | Select-Object Name, command, Location, User | Format-List
Get-ScheduledTask | Format-Table -AutoSize
Get-ScheduledTask -TaskName Office* | Format-Table -AutoSize

## Enabling / Disabling Scheduled Tasks
Disable-ScheduledTask -taskname "Adobe Flash Player Updater"
Enable-ScheduledTask -taskname "Adobe Flash Player Updater"

# Registry Entries
regedit
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
reg query HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

## Powershell Registry
get-psdrive
cd HKLM:\
set-location -path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion
Get-childitem -ErrorAction SilentlyContinue | Where-Object {$_.Name -like "*Run*"}
set-location -path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\
Get-childitem -ErrorAction SilentlyContinue | Where-Object {$_.Name -like "*Run*"}

# Active Internet Connections
netstat -ano
Get-NetTCPConnection -LocalAddress 192.168.0.100 | Sort-Object LocalPort
Get-NetTCPConnection -LocalAddress 192.168.0.100 | Select local*,remote*,state,@{Name="Process";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}} | Format-Table -AutoSize

# File Sharing
net view \\192.168.0.100
Get-SMBShare

# Files (in your user Profile)(C:\users\MyName)
cd %HOMEPATH%

## To view the .exe files with their path to locate them
forfiles /D -10 /S /M *.exe /C "cmd /c echo @path"

## To View files without its path and more details of the particular file extension and its modification date
forfiles /D -10 /S /M *.exe /C "cmd /c echo @ext @fname @fdate"

## To check for files modified in the last 10 days type
forfiles /p c: /S /D -10

## To check for file size below 6MB, you can use the file explorer’s search box and enter size:<6M

## Powershell
cd $env:userprofile
Get-ChildItem -Recurse –force -ErrorAction SilentlyContinue -Include *.exe | Sort-Object Name | Format-Table Name, Fullname -AutoSize

## Search for exe Created Last Day
Get-ChildItem -Recurse –force -ErrorAction SilentlyContinue -Include *.exe | Where-Object { $_.CreationTime -gt (Get-Date).AddDays(-1) } | Sort-Object Name | Format-Table Name, Fullname -AutoSize

## Search for exe Modified Last Day
Get-ChildItem -Recurse –force -ErrorAction SilentlyContinue -Include *.exe | Where-Object { $_.LastWriteTime -gt (Get-Date).AddDays(-1) } | Sort-Object Name | Format-Table Name, Fullname -AutoSize

# Firewall Settings

##  view the firewall configurations and the inbound and outbound traffic 
netsh firewall show config

## view the firewall settings of the current profile
netsh advfirewall show currentprofile

## Powershell
Get-NetFirewallRule | select DisplayName,Direction,Action,Enabled | Where-Object Enabled -eq $true | Sort-Object Direction, DisplayName | Format-Table -AutoSize
Get-NetFirewallProfile

# Sessions with other systems
net use

# Open Sessions
net session
Get-SmbMapping
Get-SmbConnection

# Log Entries
eventvwr.msc
Get-EventLog -List 

## Get Log From latest 2 hours
Get-EventLog Application -After (Get-Date).AddHours(-2) | Format-Table -AutoSize
Get-EventLog System -After (Get-Date).AddHours(-2) | Format-Table -AutoSize

## Search for specific message
Get-EventLog System -After (Get-Date).AddHours(-2) | Where-Object {$_.Message -like "*Server*"}

Check Windows Stability
perfmon /rel 
```
参考：https://sansorg.egnyte.com/dl/4oAuAf70Zt


### Differential Analysis
<!--rehype:wrap-class=col-span-3-->

```shell
# This assumes that there is a baseline present for services, users, scheduled tasks, and listening TCP ports. If there is no baseline available, spin up a golden image of the system and grab the baseline from that

# Capture running services, users, scheduledtasks, and listening TCP ports and then save to files
Get-Service | Select-Object -ExpandProperty Name | Out-File services.txt
Get-LocalUser | Select-Object -ExpandProperty Name | Out-File localusers.txt
Get-ScheduledTask | Select-Object -ExpandProperty TaskName | Out-File scheduledtasks.txt
Get-NetTCPConnection -State Listen | Out-File tcpports.txt

# Assign the files to variables respectively to compare with baselines
$services_current = Get-Content services.txt
$services_baseline = Get-Content services_baseline.txt

# Compare the current running services with the services from the baseline file, repeat this step for localusers, scheduledtasks, and listening TCP ports
# The output will show the difference between the two files, i.e. service running currently that were not in the baseline
Compare-Object $services_baseline $services_current
```

参考：[Differential Analysis](https://github.com/JonesPwns/powershell-incident-response/blob/main/Powershell-Incident-CheatSheet.ps1)