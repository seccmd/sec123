Windows 功能与日志
===

这个快速参考备忘单提供了使用 Windows 功能与日志 常用命令的使用清单

系统功能与日志
--------

### 检测系统信息

参数 | action
:--- | :---
`hostname` |	查看机器名
`ver` |	查看计算机操作系统版本
`set` |	查看当前机器的环境变量
`systeminfo` |  查看计算机信息（版本，位数，补丁情况） 
`whoami` | 查看当前用户及权限
`query user`     | 查看当前在线的用户 
`fsutil fsinfo drives` |      列出当前机器上的所有盘符 
`dir /a /s /b d:\"*.conf"` | 搜索d盘里conf结尾的文件 
`findstr /s /i "pass" *.py* ` | 查找文件后缀结果
`eventvwr.msc`   | 打开事件查看器

### Powershell 查询系统日志
<!--rehype:wrap-class=row-span-1 col-span-2-->

参数 | action
:--- | :--
`Get-EventLog -List`               |   查看日志清单
`Get-EventLog Security -After (Get-Date).AddHours(-2) \| Format-Table -AutoSize`               |   最近两个小时的安全日志
`Get-EventLog Security -After (Get-Date).AddHours(-2) \| Where-Object {$_.InstanceID -like "4624"}`             |    最近两个小时登录成功的日志
`Get-EventLog Security -After (Get-Date).AddHours(-2) \| Where-Object {$_.InstanceID -like "4624"} \| Format-List`       |   最近两个小时登录成功的详情
`Get-EventLog System -After (Get-Date).AddHours(-2) \| Where-Object {$_.Message -like "*Server*"}`                            |   搜索指定系统日志
`Get-EventLog Application -After (Get-Date).AddHours(-2) \| Format-Table -AutoSize`                        |   最近两个小时的应用日志
<!--rehype:className=style-list-->

WMIC
--------

### wmic 命令

参数 | action
:--- | :--
`wmic os` | 查看OS信息 
`wmic product list` | 查看安装软件
`wmic service list brief` | 查看服务 
`wmic startup list full` | 查看启动项
`wmic bios get Name,Version` | 查看bios信息
`wmic environment list` | 查看环境变量
`wmic qfe list` | 查看补丁信息 
`wmic qfe get hotfixid` | 查看补丁Patch号 
`135/tcp msrpc` | wmic 服务端口


### wmic 命令
<!--rehype:wrap-class=row-span-1 col-span-2-->

参数 | action
:--- | :--
`wmic /node:"IP" /password:"123456" /user:"admin"` | 连接目标机器 
`wmic /node:“IP” bios get /ALL` | 远程获取BIOS信息
`wmic process get caption,executablepath,commandline` | 显示进程信息
`wmic process call create "calc.exe"` | 运行程序
`wmic process where name="calc.exe" call terminate ` | 停止程序 
`wmic diskdrive get model,name,freespace,size` | 显示物理磁盘
`wmic logicaldisk where drivetype=3 get /ALL` | 显示逻辑磁盘
`wmic useraccount get /ALL ` | 显示用户信息
`wmic sysaccount list` | 显示系统账号
`wmic group list brief` | 显示用户组信息
`wmic share get name, path (or /ALL)` | 显示共享信息

WinRM
--------

### WinRM 远程管理服务

#### 参数

参数 | action
:--- | :--
`winrm quickconfig` |  开启远程管理服务
`winrm get` |        检索管理信息
`winrm set` |        修改管理信息
`winrm create` |     创建管理资源的新实例
`winrm delete` |     删除管理资源的实例
`winrm enumerate` |  列出管理资源的所有实例
`winrm identify` |   远程管理服务是否运行

#### 示例

```
# 显示运行状态，如返回报错，说明未运行
winrm e winrm/config/listener

# 启用 WinRM
winrm quickconfig

# 禁用 WinRM
winrm delete ^
winrm/config/listener?Address=*+Transport=HTTP
```

### WinRS 远程管理客户端

#### 参数

参数 | action
:--- | :--
`winrs -r` |  连接目标机器
`winrs -u` |  指定用户名
`winrs -p` |  指定密码
`winrs -d` |  指定启动目录
`winrs -env` | 指定环境变量
`winrs -ssl` | 启用 SSL 连接
`winrs -comp` | 启用压缩

#### 示例

```
# 远程管理目标机器
winrs -r:http://127.0.0.1 command 
winrs -r:https://myserver.com command 

# 配置连接信息
winrs -u:administrator -p:$%fgh7 ipconfig 
winrs -env:PATH=^%PATH^%;c:\tools

```
