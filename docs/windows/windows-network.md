Windows 网络连接
===

这个快速参考备忘单提供了使用 Windows 网络连接 常用命令的使用清单

基础网络情况
--------

### 常用命令

参数 | action
:--- | :---
`ipconfig /all`  |  获取网络信息 
`nslookup abc.com 8.8.8.8` | 解析域名信息
`route print ` | 显示路由信息
`tracert -d IP` | 追踪发包路由
`arp -a` | 查看物理地址
`at \\IP 21:31 c:\test.exe` |  定时启动应用 
`psexec \\IP -u NAME -p PWD -s CMD` |  远程执行命令

### net 命令

参数 | action
:--- | :---
`net start` |  查看开启服务
`net share` |  查看本地的共享
`net share ipc$ ` | 开启ipc$共享 
`net share ipc$ /del ` | 删除ipc$共享 
`net share c$ /del ` | 删除C：共享 
`net use \\IP\ipc$ PWD /u:NAME` | 连接目标机器
`net config workstation` | 查看域名、机器名
`net view IP` | 查看目标的共享 

### netstat 命令

参数 | action
:--- | :---
`netstat `    | 显示当前活动连接 
`netstat -a ` | 显示所有连接和侦听端口 
`netstat -n ` | 以数字形式显示地址和端口号
`netstat -o ` | 显示网络连接关联的进程 ID
`netstat -p TCP` | 指定的协议的连接
`netstat -s ` | 统计所有协议使用情况  

#### netstat 示例

```
netstat -ano
netstat -a -b
```

配置网络接口
--------

### netsh 命令1

参数 | action
:--- | :---
`netsh interface ip show config `    | 显示网络接口
`netsh interface ip show config <interface> ` | 显示指定网络接口
`netsh -c interface dump > config.txt ` | 导出网络接口配置
`netsh -f config.txt ` | 导入网络接口配置



### netsh 命令2
<!--rehype:wrap-class=row-span-1 col-span-2-->

参数 | action
:--- | :---
`netsh interface ip set address local static [ip] [netmask] [gw] 1` | 设置静态地址
`netsh interface ip set address local dhcp `    | DHCP 模式
`netsh interface ipv4 set dns <interface>  static <dns server> primary ` | DNS 配置
`netsh interface ipv4 show route `    | 显示路由
`netsh interface ipv4 add    route x.x.x.x/x <interface> <gw> ` | 添加路由
`netsh interface ipv4 delete route x.x.x.x/x <interface> <gw> ` | 删除路由


分析网络连接
--------

### 活跃的网络连接

```shell
Get-NetTCPConnection

Get-NetTCPConnection -State Established
```

### 检查开放端口

```shell
# TCP
Get-NetTCPConnection -State Listen 
# UDP
Get-NetUDPEndpoint 
```

### 仅显示外部 IP 地址

```shell
Get-NetTCPConnection | Select RemoteAddress `
-expandproperty RemoteAddress | `
Select-String  -NotMatch `
-Pattern '::', '127.0.0.1', '0.0.0.0' 
```


### 搜索特定网络连接
<!--rehype:wrap-class=row-span-1 col-span-2-->

``` shell
Get-NetTCPConnection -LocalAddress 0.0.0.0 -LocalPort 80 -RemoteAddress 0.0.0.0 -RemotePort 80
```

### 端口排序

``` shell
Get-NetTCPConnection | Sort-Object LocalPort
```

### 统计外部 IP 地址连接数
<!--rehype:wrap-class=row-span-1 col-span-3-->

```shell
Get-NetTCPConnection | Select RemoteAddress -expandproperty RemoteAddress | Select-String -Pattern '::', '127.0.0.1', '0.0.0.0'  -NotMatch `
| Sort-Object | Group-Object -NoElement | Format-Table  -AutoSize

> Output:
> Count Name
> ----- ----
>    20 10.16.215.100
>    10 10.16.78.10
>     1 10.16.79.1
```

### 检查网络连接与进程信息
<!--rehype:wrap-class=row-span-1 col-span-3-->

```shell
# 指定 TCP 端口，定位进程
Get-Process -Id (Get-NetTCPConnection -LocalPort YourPortNumberHere).OwningProcess

# 指定 UDP 端口，定位进程
Get-Process -Id (Get-NetUDPEndpoint -LocalPort YourPortNumberHere).OwningProcess

# 全部网络连接
Get-NetTCPConnection `
| Select local*,remote*,state,@{Name="Process";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}} `
| Format-Table -AutoSize
```
