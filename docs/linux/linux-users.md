Linux 用户账号
===

这个快速参考备忘单提供了使用 Linux 用户账号 常用命令的使用清单


用户账号管理
--------

### Shell 命令行

参数 | action
:--- | :---
`who` | 查看当前登录用户（tty本地登陆 pts远程登录）
`last` | 列出所有用户登陆信息
`lastb` | 列出所有用户登陆失败的信息
`lastlog` | 列出所有用户最近一次登录信息
`w` | 显示当前用户登录信息及执行的命令
`cat /etc/shadow` | 查看账户列表

### Shell 命令行

参数 | action
:--- | :---
`passwd <USERNAME>` | 修改账户密码
`passwd -l <USERNAME>` | 禁用账户
`passwd -u <USERNAME>` | 启用账户
`userdel <USERNAME>` | 删除账户
`useradd <USERNAME>` | 新建账户
