Linux 进程任务
===

这个快速参考备忘单提供了使用 Linux 进程任务 常用命令的使用清单

常用操作
---

### 进程（一）
<!--rehype:wrap-class=row-span-1-->

:--- | :---
:--- | :---
**`ps -ef `** | 显示当前活动的进程
**`ps aux \| grep 'telnet'`** | 搜索进程'telnet'的id
**`kill -9 <PID>`** | 使用给定的pid终止进程
**`top`** | 显示所有正在运行的进程
**`killall proc`** | 杀死/终止所有名为proc的进程
**`pkill process-name`** | 向具有其名称的进程发送信号
`ls -al /proc/<PID>/fd` | 查看进程文件描述符
`lsof -p <PID>` | 查看进程文件描述符
<!--rehype:className=style-list-->


### 进程（二）
<!--rehype:wrap-class=row-span-1-->

:--- | :---
:--- | :---
**`bg`** | 将一个在后台暂停的命令，变成继续执行
**`fg`** | 将后台中的命令调至前台继续运行
**`fg n`** | job n to the foreground
**`lsof`** | 列出进程打开的文件 [#](./lsof.md)
**`renice 19 PID`** | 使进程以非常低的优先级运行
**`pgrep firefox`** | 查找Firefox进程ID
**`pstree`** | 在树模型中可视化过程
**`pmap`** | 显示进程的内存映射
<!--rehype:className=style-list-->


### Shell 进程任务管理

#### 进程服务

参数 | action
:--- | :---
`systemctl` | 查看全部服务
`systemctl status <SERVICE_NAME>` | 查看服务运行状态
`systemctl stop <SERVICE_NAME>` | 关闭服务
`systemctl start <SERVICE_NAME>` | 启动服务

#### 定时任务
```
crontab -u root -l  # Root用户定时任务
cat /etc/crontab    # 系统定时任务
cat /etc/anacrontab # 系统定时任务
ls /etc/cron.*      # 系统定时任务文件
ls -la /var/spool/cron/    #  查看计划任务文件
ls -la /var/spool/anacron/ #  查看计划任务文件
```

#### 开机启动
```
cat /etc/rc.local   # 查看开机启动项
ls /etc/profile.d/  # 查看开机启动项文件
ls /etc/init.d/     # 查看开机启动项文件
ls /etc/rc.d/init.d/ # 查看开机启动项文件
```


ps 备忘清单
---

### 语法
<!--rehype:wrap-class=row-span-4-->

```bash
$ ps [options]
```

命令运行示例，列出当前 shell 中的所有进程：

```bash
$ ps

  PID TTY          TIME CMD
12330 pts/0    00:00:00 bash
21621 pts/0    00:00:00 ps
```

---

:-- | --
:-- | --
`PID` | 唯一的进程 ID
`TTY` | 用户登录的终端类型
`TIME` | 进程运行的 CPU 数量，以分钟和秒为单位
`CMD` | 启动进程的命令的名称

注意：有时当我们执行 `ps` 命令时，它显示 `TIME` 为 `00:00:00`

---

ps 命令支持 3 种使用语法风格

- `Unix` 可以分组并以连字符开头
- `BSD` 可以分组但前面没有连字符
- `GNU` 长选项，前面有双连字符

### 示例
<!--rehype:wrap-class=row-span-3-->

Option | Function
:-- | --
`ps -ef / -aux` | 以完整格式列出当前正在运行的进程
`ps -ax` | 列出当前正在运行的进程
`ps -u <username>` | 列出特定用户的进程
`ps -C <command>` | 列出给定命令的进程
`ps -p <PID>` | 列出具有给定 PID 的进程
`ps -ppid <PPID>` | 列出具有给定 ppid 的进程
`pstree` | 在层次结构中显示过程
`ps -L` | 列出特定进程的所有线程
`ps --sort pmem` | 查找内存泄漏
`ps -eo` | 显示安全信息
`ps T` | 允许您仅选择与此终端关联的所有进程
`ps -U root -u root u` | 显示由 root 运行的进程
<!--rehype:className=code-nowrap-->

### 查看系统上的每个进程

要使用标准语法查看系统上的每个进程：

```bash
$ ps -e  # 列出所有进程
$ ps -ef
$ ps -eF
$ ps -ely
```

要使用 BSD 语法查看系统上的每个进程：

```bash
$ ps ax   # 以 BSD 格式列出所有进程
$ ps axu
```

### 打印进程树

```bash
$ ps -ejH
$ ps axjf
```

### 仅打印 PID 42 的名称

```bash
$ ps -q 42 -o comm=
```

### 获取有关线程的信息

```bash
$ ps -eLf
$ ps axms
```

### 列出当前用户拥有的所有进程

```bash
$ ps x
```

### 获取安全信息
<!--rehype:wrap-class=col-span-2-->

```bash
$ ps -eo euser,ruser,suser,fuser,f,comm,label
$ ps axZ
$ ps -eM
```

### 查看以 root 身份运行的每个进程

查看以 root 身份运行的每个进程（真实且有效的 ID）用户格式：

```bash
$ ps -U root -u root u
```

### 查看具有用户定义格式的每个进程
<!--rehype:wrap-class=col-span-2-->

```bash
$ ps -eo pid,tid,class,rtprio,ni,pri,psr,pcpu,stat,wchan:14,comm
$ ps axo stat,euid,ruid,tty,tpgid,sess,pgrp,ppid,pid,pcpu,comm
$ ps -Ao pid,tt,user,fname,tmout,f,wchan
```

### 仅打印 syslogd 的进程 ID

```bash
$ ps -C syslogd -o pid=
```

### 显示面向用户的格式
<!--rehype:wrap-class=col-span-2 row-span-2-->

```bash
$ ps u

USER   PID  %CPU %MEM      VSZ    RSS   TT  STAT STARTED      TIME COMMAND
refs 11400   1.1  0.0 34853544   5816 s025  Ss   Tue02PM   0:02.82 /bin/zsh --login
refs 34561   0.6  0.0 34822644   3152 s016  S+   14Dec22 115:59.28 zsh (figterm)
refs 21377   0.5  0.0 34973972   7076 s028  S+   Wed09AM   4:32.19 zsh (figterm)
refs 78881   0.5  0.0 34843484   3256 s015  S+   17Dec22  90:27.10 zsh (figterm)
```

### 列出具有完整格式的进程

```bash
$ ps f
$ ps -F
```

### 显示虚拟内存格式

```bash
$ ps v
```

### 按有效用户 ID 或名称显示进程

```bash
$ ps -u user[name or id]
# OR
$ ps --user user[name or id]
$ ps -u root
```

按**真实**用户 ID 或名称显示进程

```bash
$ ps -U user[name or id]
# OR
$ ps --User user[name or id]
```

### 按实际组 ID 或名称显示进程

```bash
$ ps -G group[name or id]
# OR
$ ps --Group group[name or id]
```

### 隐藏 ps 命令输出的标题

```bash
$ ps h

  PID   TT  STAT      TIME COMMAND
33790 s000  S+   104:10.45 zsh (figterm)
33800 s001  Ss+    0:02.76 /bin/zsh --login
77830 s002  S+    90:22.51 zsh (figterm)
77840 s003  Ss     0:00.66 /bin/zsh --login
```

### 显示命令后的环境

```bash
$ ps e

  PID TTY      STAT   TIME COMMAND
  886 tty2     Ssl+   0:00 /usr/li....
```

### 重复 ps 命令输出的标题行

```bash
$ ps --headers -A
    PID TTY          TIME CMD
      1 ?        00:00:01 systemd
      2 ?        00:00:00 kthreadd
      3 ?        00:00:00 rcu_gp
```

### 显示进程树

```bash
$ ps --forest -A
   PID TTY          TIME CMD
     2 ?        00:00:00 kthreadd
     3 ?        00:00:00  \_ rcu_gp
     4 ?        00:00:00  \_ rcu_par_gp
   960 ?        00:00:00 \_ goa-identity-se
  1118 ?        00:00:00 \_ at-spi-bus-laun
  1124 ?        00:00:00 | \_ dbus-daemon
```

您可以使用 -H 选项打印进程层次结构

```bash
$ ps -H -A
PID TTY          TIME CMD
  2 ?        00:00:00 kthreadd
  3 ?        00:00:00   rcu_gp
1832 ?        00:00:37     gnome-terminal-
1840 pts/0    00:00:00       bash
1925 pts/1    00:00:00       bash
2867 pts/1    00:00:00         su
2868 pts/1    00:00:00           bash
```

Lsof 备忘清单
----

### 介绍

**lsof** 表示 `L`i`s`t `O`pen `F`iles 用于查找哪个进程打开了哪些文件

```shell
$ lsof
$ sudo lsof -u root
```

### 特定于端口

```shell
$ lsof -i :8080
$ lsof -i :80 -i :22
$ lsof -i TCP:22
$ lsof -i TCP:1-1024
$ lsof -i UDP
$ lsof -i @192.168.1.5
```

### 特定于进程

```shell
$ lsof -c mysql
$ lsof -c java
$ lsof -c ssh
$ lsof -c nginx
$ lsof -c ssh -c httpd
```

### 特定于用户

```shell
$ lsof -u www-data
$ lsof -u www-data -u ubuntu
$ lsof -i -u ^root # 特定用户除外
```

### 特定于网络

```shell
$ lsof -i 4   # 仅 IPv4
$ lsof -i 6   # 仅 IPv6
```

### 特定的PID

```shell
$ lsof -p 1753
$ lsof -p ^3  # 除了某些pid
```

### 特定文件名

```shell
$ lsof /var/log/messages
$ lsof /etc/passwd
```

### 特定目录

```shell
$ lsof +D /var/log # 在目录内
```

### Kill

```shell
$ kill -9 `lsof -t -u apache`
$ kill -9 $(lsof -t -i :8080)
```

### 参数
<!--rehype:wrap-class=row-span-2-->

```bash
-a        # 列出打开文件存在的进程；
-c<进程名> # 列出指定进程所打开的文件；
-g        # 列出GID号进程详情；
-d<文件号> # 列出占用该文件号的进程；
+d<目录>   # 列出目录下被打开的文件；
+D<目录>   # 递归列出目录下被打开的文件；
-n<目录>   # 列出使用NFS的文件；
-i<条件>   # 列出符合条件的进程(协议,:端口,@ip)
-p<进程号> # 列出指定进程号所打开的文件；
-u        # 列出UID号进程详情；
-h        # 显示帮助信息；
-v        # 显示版本信息
```

### 列出指定进程号所打开的文件

```bash
lsof -p $pid
```

### 获取端口对应的进程 ID=>pid

```bash
lsof -i:9981 -P -t -sTCP:LISTEN
```

### 列出打开文件的进程

```bash
lsof $filename
```

示例
---

### 示例
<!--rehype:wrap-class=col-span-2-->

```bash
$ lsof
command     PID USER   FD      type      DEVICE     SIZE       NODE NAME
init          1 root  cwd       DIR         8,2     4096          2 /
init          1 root  rtd       DIR         8,2     4096          2 /
init          1 root  txt       REG         8,2    43496    6121706 /sbin/init
init          1 root  mem       REG         8,2   143600    7823908 /lib64/ld-2.5.so
init          1 root  mem       REG         8,2  1722304    7823915 /lib64/libc-2.5.so
init          1 root  mem       REG         8,2    23360    7823919 /lib64/libdl-2.5.so
init          1 root  mem       REG         8,2    95464    7824116 /lib64/libselinux.so.1
init          1 root  mem       REG         8,2   247496    7823947 /lib64/libsepol.so.1
init          1 root   10u     FIFO        0,17                1233 /dev/initctl
migration     2 root  cwd       DIR         8,2     4096          2 /
migration     2 root  rtd       DIR         8,2     4096          2 /
migration     2 root  txt   unknown                                 /proc/2/exe
```

### 文件描述符列表(FD)
<!--rehype:wrap-class=row-span-3-->

:- | :-
:- | :-
`cwd`  | 表示当前工作目录，即：应用程序的当前工作目录，这是该应用程序启动的目录，除非它本身对这个目录进行更改
`txt`  | 该类型的文件是程序代码，如应用程序二进制文件本身或共享库，如上列表中显示的 /sbin/init 程序
`lnn`  | 库引用 (AIX);
`er`   | FD 信息错误（参见名称栏）
`jld`  | jail 目录 (FreeBSD);
`ltx`  | 共享库文本（代码和数据）
`mxx`  | 十六进制内存映射类型编号xx
`m86`  | DOS合并映射文件
`mem`  | 内存映射文件
`mmap` | 内存映射设备
`pd`   | 父目录
`rtd`  | 根目录
`tr`   | 内核跟踪文件 (OpenBSD)
`v86`  | VP/ix 映射文件
`0`    | 表示标准输出
`1`    | 表示标准输入
`2`    | 表示标准错误
<!--rehype:className=style-list-arrow-->

### 示例列信息

:- | :-
:- | :-
`COMMAND` | 进程的名称
`PID` | 进程标识符
`PPID` | 父进程标识符（需要指定-R参数）
`USER` | 进程所有者
`PGID` | 进程所属组
`FD` | 文件描述符，应用程序通过它识别该文件

### 标准输出/输入/错误文件状态模式(FD)

:- | :-
:- | :-
`u` | 表示该文件被打开并处于读取/写入模式
`r` | 表示该文件被打开并处于只读模式
`w` | 表示该文件被打开并处于写入模式
`空格` | 表示该文件的状态模式为 unknow，且没有锁定
`-` | 表示该文件的状态模式为 unknow，且被锁定

一般在[标准输出/输入/错误](#文件描述符列表fd)后还跟着文件状态模式

### 文件状态模锁 (FD)

:- | :-
:- | :-
`N`     | 对于未知类型的Solaris NFS锁
`r`     | 用于部分文件的读取锁定
`R`     | 对整个文件进行读取锁定
`w`     | 对文件的一部分进行写锁定(文件的部分写锁)
`W`     | 对整个文件进行写锁定(整个文件的写锁)
`u`     | 用于任何长度的读写锁
`U`     | 对于未知类型的锁
`x`     | 对于文件部分的SCO OpenServer Xenix锁
`X`     | 对于整个文件的SCO OpenServer Xenix锁
`space` | 如果没有锁

在[文件状态模式](#标准输出输入错误文件状态模式fd)后面，还跟着相关的锁

### 文件类型

标识 | 说明
:- | :-
`DIR` | 表示目录
`CHR` | 表示字符类型
`BLK` | 块设备类型
`UNIX` |  UNIX 域套接字
`FIFO` | 先进先出 (FIFO) 队列
`IPv4` | 网际协议 (IP) 套接字
`DEVICE` | 指定磁盘的名称
`SIZE` | 文件的大小
`NODE` | 索引节点（文件在磁盘上的标识）
`NAME` | 打开文件的确切名称
`REG` | 常规文件

另见
---

- [lsof 命令帮助文档](https://jaywcjlove.github.io/linux-command/c/lsof.html) _(jaywcjlove.github.io)_


htop 备忘清单
----

### htop 用法

htop 是一个互动的进程查看器，动态观察系统进程状况

- [命令 htop 的官网](https://htop.sourceforge.net/)

```bash
$ htop [-dChustv]
```

#### 安装

```bash
$ apt install htop        # Debian
$ dnf install htop        # Fedora
$ emerge sys-process/htop # Gentoo
$ pacman -S htop          # Arch Linux
$ Compile htop            # GoboLinux
```

htop 的软件包在大多数发行版中都[可用下载](https://htop.dev/downloads.html)

### 选项示例
<!--rehype:wrap-class=col-span-2-->

长选项的强制参数对于短选项也是强制的

:- | :-
:- | :-
`-d --delay=DELAY` | 更新之间的延迟，以十分之一秒为单位
`-C --no-color --no-colour` | 以单色模式启动 `htop`
`-h --help` | 显示帮助消息并退出
`-p --pid=PID,PID...` | 仅显示给定的PID
`-s --sort-key COLUMN` | 按此列排序(对列列表使用`--sort-key`帮助)
`-u --user=USERNAME` | 仅显示给定用户的进程
`-v --version` | 输出版本信息并退出
`-t --tree` | 在树状视图中显示流程

### 状态

:- | :-
:- | :-
`R`  | 运行中
`S`  | 休眠
`T`  | 追踪/停止
`Z`  | 僵尸
`D`  | 磁盘睡眠
<!--rehype:className=shortcuts-->

### 交互式命令
<!--rehype:wrap-class=col-span-2 row-span-3-->

:- | :-
:- | :-
`F1`, `h`, `?` | 转到帮助屏幕
`F10`, `q` | 退出
`Space` | 标记或取消标记进程
`U` | 取消标记所有进程(删除所有使用 Space 键添加的标记)
`s` | 跟踪进程系统调用：如果安装了 `strace(1)`，按下此键会将其附加到当前选定的进程，呈现进程发出的系统调用的实时更新
`l` | 显示进程打开的文件：如果安装了 `lsof(1)`，按下该键将显示进程打开的文件描述符列表
`F2`, `S` | 转到设置屏幕，您可以在其中配置屏幕顶部显示的仪表，设置各种显示选项，在配色方案中进行选择，并选择显示的列，以何种顺序显示
`F3`, `/` | 逐步搜索所有显示进程的命令行。当前选定(突出显示)的命令将在您键入时更新。在搜索模式下，按 `F3` 将循环匹配出现的事件
`F4`, `\` | 增量进程过滤：输入部分进程命令行，仅显示名称匹配的进程。要取消过滤，请再次输入过滤选项并按 `Esc`
`F5`, `t` | 树视图：按父级组织进程，并将它们之间的关系布局为树。切换键将在树和您之前选择的排序视图之间切换。选择排序视图将退出树视图
`F6` | 在排序视图上，选择一个字段进行排序，也可以通过 < 和 > 访问。当前排序字段由标题中的突出显示。在树视图中，展开或折叠当前子树。树节点中的“+”指示符表示它已折叠
`F7`, `]` | 增加所选进程的优先级(从“nice”值中减去)。这只能由超级用户完成
`F8`, `[` | 降低选定进程的优先级(添加到“nice”值)
`F9`, `k` | “杀死”进程：向一个或一组进程发送一个在菜单中选择的信号。如果进程被标记，则将信号发送到所有标记的进程。如果没有标记，则发送到当前选定的进程
`+`, `-` | 在树视图模式下，展开或折叠子树。
`a` | (在多 CPU 机器上)设置 CPU 亲和性：标记允许进程使用的 CPU
`u` | 仅显示指定用户拥有的进程
`F` | “跟随”进程：如果排序顺序导致当前选定的进程在列表中移动，则使选择栏跟随它。这对于监控进程很有用：这样，您可以使进程始终在屏幕上可见。使用移动键时，“跟随”失效。
`p` | 在适用的情况下显示运行程序的完整路径(这是一个切换键)
`Ctrl-L` | 刷新：重绘屏幕并重新计算数值
`Numbers` | PID搜索：输入进程ID，选择突出显示将移至它
<!--rehype:className=shortcuts-->

### 排序/线程

:- | :-
:- | :-
`M` | 按`内存`使用情况排序 _(最高兼容性键)_
`P` | 按`CPU`使用情况排序 _(最高兼容性键)_
`T` | 按`时间`排序 _(最高兼容性键)_
`I` | `反转`排序顺序
`K` | 隐藏`内核`线程
`H` | 隐藏`用户`线程
<!--rehype:className=shortcuts-->

### 滚动

:- | :-
:- | :-
`Up`, `Alt-k` | 在流程列表中选择(突出)`上`一个流程
`Down`, `Alt-j` | 在流程列表中选择(突出)`下`一个流程
`Left`, `Alt-h` | 向`左`滚动流程列表
`Right`, `Alt-l` | 向`右`滚动进程列表
`PgUp`, `PgDn` | 将流程列表`向上`或`向下`滚动一个窗口
`Home` | 滚动到流程列表的`顶部` <br /> _选择第一个流程_
`End` | 滚动到流程列表的`底部` <br /> _选择最后一个流程_
`Ctrl-A`, `^` | 向`左`滚动到流程条目`开头` _(即行开头)_
`Ctrl-E`, `$` | 向`右`滚动到流程条目`末尾` _(即行尾)_
<!--rehype:className=shortcuts-->

Systemd 备忘清单
----

### 查看系统信息

:- | -
:- | -
`systemctl list-dependencies` | 显示单元的依赖关系
`systemctl list-sockets` | 列出套接字和激活的内容
`systemctl list-jobs` | 查看活动的 systemd 作业
`systemctl list-unit-files` | 查看单元文件及其状态
`systemctl list-units` | 显示单位是否已加载/活动
`systemctl get-default` | 列出默认目标(如运行级别)
<!--rehype:className=style-list-->

### 改变系统状态

:- | -
:- | -
`systemctl reboot` | 重启系统(reboot.target)
`systemctl poweroff` | 关闭系统(poweroff.target)
`systemctl emergency` | 进入紧急模式(emergency.target)
`systemctl default` | 返回默认目标(multi-user.target)
<!--rehype:className=style-list-->

### 使用服务
<!--rehype:wrap-class=row-span-2-->

:- | -
:- | -
`systemctl stop service` | <red>停止</red>正在运行的服务
`systemctl start service` | 启动服务
`systemctl restart service` | 重新启动正在运行的服务
`systemctl reload service` | 重新加载服务中的所有配置文件
`systemctl daemon-reload` | 必须运行以重新加载更改的单元文件
`systemctl status` | service 查看服务是否正在运行/启用
`systemctl --failed` | 显示未能运行的服务
`systemctl reset-failed` | 将任何单位从失败状态重置
`systemctl enable service` | 使服务在启动时启动
`systemctl disable service` | 禁用服务 - 不会在启动时启动
`systemctl show service` | 显示服务(或其他单元)的属性
`systemctl edit service` | 创建片段以放入单元文件
`systemctl edit --full service` | 编辑整个单元文件以进行服务
`systemctl -H host status network` | 远程运行任何 systemctl 命令
<!--rehype:className=style-list-->

### 查看日志消息
<!--rehype:wrap-class=col-span-2-->

:- | -
:- | -
`journalctl` | 显示所有收集的日志消息
`journalctl -u network.service` | 查看网络服务消息
`journalctl -f` | 关注出现的消息
`journalctl -k` | 仅显示内核消息

### SysVinit 到 Systemd
<!--rehype:wrap-class=col-span-3-->

SysVinit | Systemd | 说明
:- | - | -
`service SERVICE_NAME start` | `systemctl start SERVICE_NAME` | 用于启动服务(不重启持久)
`service SERVICE_NAME stop` | `systemctl stop SERVICE_NAME` | 用于停止服务(不永久重启)
`service SERVICE_NAME restart` | `systemctl restart SERVICE_NAME` | 用于停止然后启动服务
`service SERVICE_NAME reload` | `systemctl reload SERVICE_NAME` | 重新加载配置文件而不中断挂起的操作
`service SERVICE_NAME condrestart` | `systemctl condrestart SERVICE_NAME` | 如果服务已在运行，则重新启动
`service SERVICE_NAME status` | `systemctl status SERVICE_NAME` | 判断服务当前是否正在运行
`chkconfig SERVICE_NAME on` | `systemctl enable SERVICE_NAME` | 打开服务，以便在下次启动时启动，或其他触发器
`chkconfig SERVICE_NAME off` | `systemctl disable SERVICE_NAME` | 为下次重新启动或任何其他触发器关闭服务
`chkconfig SERVICE_NAME` | `systemctl is-enabled SERVICE_NAME` | 用于检查服务是否配置为在当前环境中启动
`chkconfig –list` | `systemctl list-unit-files –type=service` (or) <br/>`ls /etc/systemd/system/*.wants/` | 打印一个服务表，列出每个配置的运行级别打开或关闭
`chkconfig –list \| grep 5:on` | `systemctl list-dependencies graphical.target` | 打印启动到图形模式时将启动的服务表
`chkconfig SERVICE_NAME –list` | `ls /etc/systemd/system/*.wants/SERVICE_NAME.service` | 用于列出此服务配置为打开或关闭的级别
`chkconfig SERVICE_NAME –add` | `systemctl daemon-reload` | 在创建新服务文件或修改任何配置时使用
<!--rehype:className=show-header-->

### 目标运行级别
<!--rehype:wrap-class=col-span-3-->

SysVinit | Systemd | 说明
:- | - | -
`0` | `runlevel0.target`, `poweroff.target` | 停止系统
`1`, `s`, `single` | `runlevel1.target`, `rescue.target` | 单用户模式
`2`, `4` | `runlevel2.target`, `runlevel4.target`, `multi-user.target` | 用户定义/站点特定的运行级别。 默认情况下，与 3 相同
`3` | `runlevel3.target`, `multi-user.target` | 多用户，非图形。 用户通常可以通过多个控制台或通过网络登录
`5` | `runlevel5.target`, `graphical.target` | 多用户，图形。 通常具有运行级别 3 的所有服务以及图形登录
`6` | `runlevel6.target`, `reboot.target` | 重启
`emergency` | `emergency.target` | 应急外壳
<!--rehype:className=show-header-->

### 更改运行级别
<!--rehype:wrap-class=col-span-3-->

SysVinit | Systemd | 说明
:- | - | -
`telinit 3` | `systemctl isolate multi-user.target` <br/>OR `systemctl isolate runlevel3.target`<br/>OR `telinit 3` | 更改为多用户运行级别
`sed s/^id:.*:initdefault:/id:3:initdefault:/` | `ln -sf /lib/systemd/system/multi-user.target /etc/systemd/system/default.target` | 设置为在下次重新启动时使用多用户运行级别
<!--rehype:className=show-header-->

另见
---

- [Systemd 官网](https://systemd.io/) _(systemd.io)_
- [Systemd Cheat Sheet](https://access.redhat.com/sites/default/files/attachments/12052018_systemd_6.pdf) _(access.redhat.com)_
- [Systemd Cheat Sheet](https://www.linuxtrainingacademy.com/systemd-cheat-sheet/) _(linuxtrainingacademy.com)_


Cron 备忘清单
------
<!--rehype:body-class=cols-2-->

### 格式

```
Min  Hour Day  Mon  Weekday
分钟  小时  天   月   周
```

-------

```bash
*    *    *    *    *   <要执行的命令>
┬    ┬    ┬    ┬    ┬
│    │    │    │    └─  星期几         (0=周日 .. 6=星期六)
│    │    │    └──────  月            (1..12)
│    │    └───────────  月份中的某天    (1..31)
│    └────────────────  小时           (0..23)
└─────────────────────  分钟           (0..59)
```

-------

| 字段          | 范围   | 特殊字符             |
|--------------|--------|--------------------|
| 分钟 Minute   | 0 - 59 | <kbd>,</kbd> <kbd>-</kbd> <kbd>*</kbd> <kbd>/</kbd>
| 小时 Hour     | 0 - 23 | <kbd>,</kbd> <kbd>-</kbd> <kbd>*</kbd> <kbd>/</kbd>
| 月份中的某天   | 1 - 31 | <kbd>,</kbd> <kbd>-</kbd> <kbd>*</kbd> <kbd>?</kbd> <kbd>/</kbd> <kbd>L</kbd> <kbd>W</kbd>
| 月 Month     | 1 - 12 | <kbd>,</kbd> <kbd>-</kbd> <kbd>*</kbd> <kbd>/</kbd>
| 星期几        | 0 - 6  | <kbd>,</kbd> <kbd>-</kbd> <kbd>*</kbd> <kbd>?</kbd> <kbd>/</kbd> <kbd>L</kbd> <kbd>#</kbd>
| 年 Year       | 1970–2099  | <kbd>,</kbd> <kbd>-</kbd>
<!--rehype:className=show-header-->

### 示例

| Example        | Description            |
|----------------|------------------------|
| `*/15 * * * *` | 每 15 分钟   |
| `0 * * * *`    | 每隔一小时   |
| `0 */2 * * *`  | 每 2 小时   |
| `15 2 * * *`   | 每天凌晨 2 点 15 分   |
| `15 2 * * ?`   | 每天凌晨 2 点 15 分   |
| `10 9 * * 5`   | 每周五上午 9:10   |
| `0 0 * * 0`    | 每个星期日的午夜   |
| `15 2 * * 1L`  | 每月最后一个星期一凌晨 2 点 15 分   |
| `15 0 * * 4#2` | 每个月的第二个星期四早上 00:15   |
| `0 0 0 1 * *`  | 每个月的 1 日(每月)   |
| `0 0 0 1 1 *`  | 每年 1 月 1 日(每年)   |
| `@reboot`      | 每次重启 _(非标准)_   |

### 特殊字符串

| 特殊字符串       | 意义                                            |
|----------------|----------------------------------------------------|
| @reboot        | 运行一次，在系统启动时 _(非标准)_ |
| @yearly        | 每年运行一次，“0 0 1 1 *” _(非标准)_ |
| @annually      | (与@yearly 相同)_(非标准)_ |
| @monthly       | 每月运行一次，“0 0 1 \* \*” _(非标准)_ |
| @weekly        | 每周运行一次，“0 0 \* \* 0” _(非标准)_ |
| @daily         | 每天运行一次，“0 0 \* \* \*” _(非标准)_ |
| @midnight      | (与@daily 相同)_(非标准)_ |
| @hourly        | 每小时运行一次，“0 \* \* \* \*” _(非标准)_ |
<!--rehype:className=show-header -->

### Crontab 命令

| -            | -                                           |
|--------------|---------------------------------------------|
| `crontab -e` | 如果不存在，则编辑或创建一个 crontab 文件       |
| `crontab -l` | 显示 crontab 文件 |
| `crontab -r` | 删除 crontab 文件 |
| `crontab -v` | 显示您上次编辑 crontab 文件的时间 _(非标准)_ |

轻松添加任务

```bash
echo "@reboot echo hi" \| crontab
```

### 特殊字符
<!--rehype:wrap-class=col-span-2-->

| 特殊字符             | 说明 |
|---------------------|------------|
`星号(*)`  | 匹配字段中的所有值或任何可能的值。
`横杆(-)`  | 用于定义范围。例如：第 5 个字段(星期几)中的 1-5 每个工作日，即星期一到星期五
`斜线 (/)` | 第一个字段(分钟)/15 表示每十五分钟或范围的增量。
`逗号(,)`  | 用于分隔项目。例如：第二个字段(小时)中的 2、6、8 在凌晨 2 点、早上 6 点和早上 8 点执行
`L`       | 仅允许用于 `月份中的某天` 或 `星期几` 字段，`星期几` 中的 `2L` 表示每个月的最后一个星期二
`井号 (#)` | 仅允许用于 `星期几` 字段，后面必须在 1 到 5 的范围内。例如，`4#1` 表示给定月份的“第一个星期四”。
`问号(?)`  | 可以代替“*”并允许用于月份和星期几。使用仅限于 cron 表达式中的 `月份中的某天` 或 `星期几`。
<!--rehype:className=show-header auto-wrap-->

另见
----

- [Devhints](https://devhints.io/cron) _(devhints.io)_
- [Crontab Generator](https://crontab-generator.org/) _(crontab-generator.org)_
- [Crontab guru](https://crontab.guru/) _(crontab.guru)_

