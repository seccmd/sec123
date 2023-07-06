Linux 系统日志
===

这个快速参考备忘单提供了使用 Linux 系统日志 常用命令的使用清单

系统日志管理
--------

参考：[linux-logs](https://www.socinvestigation.com/linux-audit-logs-cheatsheet-detect-respond-faster/)


### 日志（一）

参数 | action
:--- | :---
`/var/log/messages` | Redhat/CentrOS 系统日志
`/var/log/syslog `  | Debian/Ubuntu 安全日志
`/var/log/secure`   | Redhat/CentrOS 安全日志
`/var/log/auth.log` | Debian/Ubuntu 安全日志
`/var/log/cron`     | 定时任务日志

### 日志（二

参数 | action
:--- | :---
`/var/log/boot.log` | 启动引导日志
`/var/log/kern`     | 内核告警日志
`/var/log/dmesg`    | 设备驱动日志
`var/log/mail.log`  | 邮件服务日志
`/var/log/daemon.log` | 后台服务日志

### 日志（三）

参数 | action
:--- | :---
`/var/log/lastlog` | 跟踪每次登录/注销
`/var/log/faillog` | 跟踪失败的登录尝试
`/var/log/btmp` | 记录所有失败的登录尝试
`/var/log/utmp` | 跟踪用户当前的登录状态
`/var/log/wtmp` | 跟踪每次登录和注销

日志处理工具
--------

### grep 命令

GREP allows you to search patterns in files.

```bash
-v: Invert matches
-i: Case insensitive
-E: Extended regex
-c: Count number of matches

$ grep <pattern> file.log
```

### cut 命令

CUT is used to parse fields from delimited logs

```bash
-d: Use the field delimiter
-f: The field numbers
-c: Specifies characters position

$ cut -d ":" -f 2 file.log
```

### shell 命令

SORT is used to sort a file

```bash
# -r: Reverse order
$ sort file.log
```

UNIQ is used to extract uniq occurrences

```bash
# -c: Count number of duplicates
$ uniq -c file.log
```


### awk 命令

AWK is used to manipulate data

```bash
# Print first column with separator ":"
$ awk -F : '{print $1}' file.log

# 累加第一列的值
$ awk '{a+=$1}END{print a}'
```

### sed 命令

SED (Stream Editor) is used to replace strings in a file.

```bash
# s: Search
# g: Replace
# d: Delete

$ sed s/regex/replace/g
```

### diff 命令

DIFF differences in files by compare

```bash
$ diff 1.log 2.log 
# How to read output?
a: Add    #: Line numbers
c: Change <: File 1
d: Delete >: File 2
```
