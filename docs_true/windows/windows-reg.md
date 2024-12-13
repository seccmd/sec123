Windows 注册表
===

这个快速参考备忘单提供了使用 Windows 注册表 常用命令的使用清单

注册表管理
--------

### CMD 命令行
<!--rehype:wrap-class=row-span-1 col-span-3-->

action | 参数
:--- | :---
查询注册表操作 | `reg query HKEY_CURRENT_USER\Software`
添加注册表操作 | `reg add HKEY_CURRENT_USER\Software /v "Name" /t REG_SZ /d "Data" /f`
删除注册表项操作 | `reg delete HKEY_CURRENT_USER\Software /v "Name" /f`
导出注册表项的内容 | `reg export HKEY_CURRENT_USER\Software C:\test.reg`
导入注册表项 | `reg import C:\test.reg`
远程访问注册表 | `reg export \\[ip]\ [domain]\[key] output.reg`
导出用户组信息、权限配置 | `reg save HKLM\SAM sam.hive `
导出SYSKEY | `reg save HKLM\SYSTEM system.hive `
搜集注册表中的各种密码数据 | `reg query HKLM /f password /t REG_SZ /s`
查看有没有开启远程链接 (结果：1表示关闭，0表示开启 ) | `REG QUERY "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections `
<!--rehype:className=style-list-->

参考：[cmd-reg](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/reg)


### Powershell 命令行
<!--rehype:wrap-class=row-span-1 col-span-3-->

```
# 查询注册表项名称
Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion |
    Select-Object -ExpandProperty Property

# 查询注册表项数据
Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion

# 指定注册表项数据
Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath

# 进入注册表目录
Set-Location -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion

# 查询当前路径
Get-ItemProperty -Path .

# 搜索注册表项
Get-ChildItem -ErrorAction SilentlyContinue \| Where-Object {$_.Name -like "*Run*"}
```

参考：[ps-registry](https://learn.microsoft.com/zh-cn/powershell/scripting/samples/working-with-registry-entries?view=powershell-7.3)


