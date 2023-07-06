Windows 用户账号
===

这个快速参考备忘单提供了使用 Windows 用户账号 常用命令的使用清单

用户账号管理
--------

### Powershell 命令行

参数 | action
:--- | :---
`Get-LocalUser`   | 查账户列表
`Disable-LocalUser <USERNAME>` | 禁用账户
`Enable-LocalUser <USERNAME>` | 启用账户
`Remove-LocalUser -Name <USERNAME>` | 删除账户
`New-LocalUser -Name <USERNAME> -NoPassword` | 新建账户
`Rename-LocalUser -Name <USERNAME>` | 修改账户
`Set-LocalUser -Name <USERNAME>` | 编辑账户
`Get-LocalGroupMember Administrators` |

### CMD 命令行

参数 | action
:--- | :---
`net user`   | 账户列表
`net user <USERNAME> /active:no` | 禁用账户
`net user <USERNAME> /active:yes` | 启用账户
`net user <USERNAME> /del` | 删除账户
`net user <USERNAME> <PASSWORD> /add` | 新建账户
`net user <USERNAME> <PASSWORD>` |  修改密码
`net user 用户名 密码 /add` | 建立用户 
`net user 用户名 /del` | 删除用户 
`net user guest /active:yes` | 激活guest账户 

### CMD 命令行

参数 | action
:--- | :---
`net user 账户名` | 查看指定账户信息 
`net user /domain` | 查看域内有哪些用户
`net user 用户名 /domain` | 查看账户信息 
`net group /domain` | 查看域中的组 
`net group "domain admins" /domain` | 查看当前域的管理用户 
`net localgroup` | 查看所有的本地组 
`net localgroup administrators` | 查看管理员组中有哪些用户 
`net localgroup administrators 用户名 /add` | 把用户添加到管理员组中 


域控信息
--------

### CMD 命令行

参数 | action
:--- | :---
`dsquery server ` | 查看所有域控制器 
`dsquery subnet ` | 查看域内内子网 
`dsquery group  ` | 查看域内工作组 
`dsquery site   ` | 查看域内站点 
`net time /domain` |	查看域名、时间
`net view /domain` |	查看域内所有共享
