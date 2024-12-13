Linux 系统命令
===

这个快速参考备忘单提供了使用 Linux 常用命令的使用清单

用户管理
--------

### 用户信息

:--- | :---
:--- | :---
**`id`** | 显示活动用户的详细信息，如uid、gid和组
**`who`** | 显示谁已登录到系统
**`last`** | 显示系统中的最后一次登录
`w` | 显示当前用户登录信息及执行的命令
`lastb` | 列出所有用户登陆失败的信息
`lastlog` | 列出所有用户最近一次登录信息


### 用户操作

参数 | action
:--- | :---
**`groupadd "admin"`** | 添加组"admin"
**`adduser "Sam"`** | 添加用户 Sam
**`userdel "Sam"`** | 删除用户 Sam
**`usermod`** | 用于更改/修改用户信息
`userdel <USERNAME>` | 删除账户
`useradd <USERNAME>` | 新建账户

### passwd 命令

参数 | action
:--- | :---
`passwd <USERNAME>` | 修改账户密码
`passwd -l <USERNAME>` | 禁用账户
`passwd -u <USERNAME>` | 启用账户
`cat /etc/shadow` | 查看账户列表


命令速查表
---

### 系统
<!--rehype:wrap-class=row-span-2-->

:--- | :---
:--- | :---
**`uname`** | 显示linux系统信息
**`uname -r`** | 显示内核版本信息
**`uptime`** | 显示系统运行的时间<br/>(包括平均负载)
**`hostname`** | 显示系统主机名
**`hostname -i`** | 显示系统的IP地址
**`last reboot`** | 显示系统重新启动历史记录
**`date`** | 显示当前系统日期和时间
**`timedatectl`** | 查询和更改系统时钟
**`cal`** | 显示当前日历的月份和日期
**`w`** | 显示系统中当前登录的用户
**`whoami`** | 显示您的登录身份
**`finger username`** | 显示有关用户的信息
<!--rehype:className=style-list-->

### 硬件
<!--rehype:wrap-class=row-span-2-->

:--- | :---
:--- | :---
**`dmesg`** | 显示启动消息
**`cat /proc/cpuinfo`** | 显示有关CPU的更多信息，例如型号、型号名称、核心、厂商标识
**`cat /proc/meminfo`** | 显示有关硬件内存的更多信息，例如总内存和可用内存
**`lshw`** | 显示有关系统硬件配置的信息
**`lsblk`** | 显示块设备相关信息
**`free -m`** | 显示系统中空闲和使用的内存(-m标志表示内存(MB))
**`lspci -tv`** | 在树状图中显示PCI设备
**`lsusb -tv`** | 以树状图的形式显示USB设备
**`dmidecode`** | 显示BIOS中的硬件信息
**`hdparm -i /dev/xda`** | 显示有关磁盘数据的信息
**`hdparm -tT /dev/xda <:code>`** | 在设备xda上进行读速度测试
**`badblocks -s /dev/xda`** | 测试磁盘上不可读的块
<!--rehype:className=style-list-->



### 登陆

:--- | :---
:--- | :---
**`ssh user@host`** | 使用指定用户安全连接到主机
**`ssh -p port_number user@host`** | 使用指定端口安全地连接到主机
**`ssh host`** | 通过SSH默认端口22安全连接到系统
**`telnet host`** | 通过telnet默认端口23连接到主机
<!--rehype:className=style-list-->

### 文件
<!--rehype:wrap-class=row-span-3-->

:--- | :---
:--- | :---
**`ls -al`** | 列出文件-包括常规文件和隐藏文件以及它们的权限
**`pwd`** | 显示当前目录文件路径
**`mkdir 'directory_name'`** | 创建一个新目录
**`rm file_name`** | 删除一个文件
**`rm -f filename`** | 强制删除文件
**`rm -r directory_name`** | 递归地删除一个目录
**`rm -rf directory_name`** | 强制并递归地删除一个目录
**`cp file1 file2`** | 将file1的内容复制到file2
**`cp -r dir1 dir2`** | 递归地将dir1复制到dir2。如果dir2不存在，则创建它
**`mv file1 file2`** | 将file1重命名为file2
**`ln -s /path/to/file_name link_name`** | 创建到file_name的软链接
**`touch file_name`** | 创建一个新文件
**`cat > file_name`** | 从键盘创建一个文件
**`more file_name`** | 输出文件的内容
**`head file_name`** | 显示文件的前10行
**`tail file_name`** | 显示文件的最后10行
**`gpg -c file_name`** | 加密一个文件
**`gpg file_name.gpg`** | 解密文件
**`wc`** | 打印文件中的字节、单词和行数
**`xargs`** | 从标准输入执行命令
<!--rehype:className=style-list-->


### 文件权限

:--- | :---
:--- | :---
**`chmod octal filename`** | 将文件权限更改为八进制
**`chmod 777 /data/test.c`** | 将rwx权限设置为owner、group和everyone(其他可以访问服务器的人)
**`chmod 755 /data/test.c`** | 将rwx设置为所有者，将r_x设置为组和所有人
**`chmod 766 /data/test.c`** | 为所有者设置rwx，为组和每个人设置rw
**`chown owner user-file`** | 更改文件的所有权
**`chown owner-user:owner-group file_name`** | 更改文件的所有者和组所有者
**`chown owner-user:owner-group directory`** | 更改目录的所有者和组所有者
<!--rehype:className=style-list-->


### 压缩/打包

:--- | :---
:--- | :---
**`tar -cf home.tar home<:code>`** | 创建名为"home"的存档文件。tar文件’home'
**`tar -xf files.tar`** | 解压档案文件"files.tar"
**`tar -zcvf home.tar.gz source-folder`** | 从源文件夹创建压缩的tar存档文件
**`gzip file`** | 压缩扩展名为.gz的文件
<!--rehype:className=style-list-->

### 搜索

:--- | :---
:--- | :---
**`grep ‘pattern’ files`** | 在文件中搜索给定的模式
**`grep -r pattern dir`** | Search recursively for a pattern in a given directory
**`locate file`** | 查找文件的所有实例
**`find /home/ -name "index"`** | 在/home文件夹中查找以’index’开头的文件名
**`find /home -size +10000k`** | 在主文件夹中查找大于10000k的文件
<!--rehype:className=style-list-->


### 磁盘使用情况
<!--rehype:wrap-class=row-span-1-->

:--- | :---
:--- | :---
**`df -h`** | 显示安装系统上的空闲空间
**`df -i`** | 显示文件系统上的空闲inode
**`fdisk -l`** | 显示磁盘分区、大小和类型
**`du -sh`** | 以人类可读的格式显示当前目录中的磁盘使用情况
**`findmnt`** | 显示所有文件系统的目标挂载点
**`mount device-path mount-point`** | 挂载设备
<!--rehype:className=style-list-->


另见
---

- [Linux命令大全搜索工具](https://jaywcjlove.github.io/linux-command) _(jaywcjlove.github.io)_
- [Linux命令大全(手册)](https://www.linuxcool.com/) _(linuxcool.com)_
- [MAN手册 - 中文](https://manpages.debian.org/buster/manpages-zh/index.html) _(debian.org)_
- [Linux 命令行速查表](https://www.cheat-sheet.cn/post/linux-command-line-cheat-sheet/) _(cheat-sheet.cn)_


YUM 清单查询
---

### 介绍

yum（`Y`ellow dog `U`pdater, `M`odified）是一个在 `Fedora` 和 `RedHat` 以及 SUSE 中的 `Shell` 前端软件包管理器

```bash
$ yum [options] [command] [package ...]
```

----

- [YUM 官方网站](http://yum.baseurl.org/) _(yum.baseurl.org)_
- [Fedora 中的 Yum 文档](https://docs.fedoraproject.org/en-US/Fedora/15/html/Deployment_Guide/ch-yum.html) _(fedoraproject.org)_
- [CentOS 中的 Yum 文档](http://wiki.centos.org/PackageManagement/Yum/) _(wiki.centos.org)_
- [Scientific Linux 中的 Yum 文档](https://www.scientificlinux.org/documentation/faq/yum.apt.repo) _(scientificlinux.org)_

### YUM 查询

子命令描述和任务

#### help

显示 yum 命令和选项

```bash
yum help
```

显示 yum 子命令和选项

### 单独的包
<!--rehype:wrap-class=row-span-3-->

#### list

列出存储库中的包名称

```bash
# 列出存储库中的包名称
yum list available
# 列出所有可用的包
yum list installed
# 列出所有已安装的包
yum list all
# 列出已安装和可用的软件包
yum list kernel
```

#### info

列出已安装和可用的内核包

```bash
# 列出有关 `vsftpd` 软件包的信息
$ yum info vsftpd
```

#### deplist

显示包的依赖项

```bash
$ yum deplist nfs-utils
```

列出依赖项和提供它们的包

#### provides

```bash
# 查找提供查询文件的包
$ yum provides “*bin/top”
# 显示包含 README.top 文件的包
$ yum provides “*/README.top”
```

#### search

```bash
# 查找名称或描述中带有 samba 的软件包
$ yum search samba
```

#### updateinfo

```bash
# 获取有关可用软件包更新的信息
$ yum updateinfo security
```

获取有关可用 security 更新的信息

### 包组

#### grouplist

列出已安装和可用软件包组的名称

#### groupinfo

```bash
# 查看 Web 服务器组中的包
$ yum groupinfo "Web Server"
```

#### check-update

查询存储库以获取可用的软件包更新

### 管理 YUM 存储库
<!--rehype:wrap-class=row-span-2-->

#### repolist

显示启用的软件存储库

#### repoinfo

显示有关启用的 `yum` 存储库的信息 *

```bash
$ yum repoinfo rhel-7-server-rpms
```

请参阅有关 rhel-7-server-rpms 存储库的信息

#### repo-pkgs

使用特定存储库中的包 *

```bash
# 列出来自 my-rpms 存储库的软件包
$ yum repo-pkgs my-rpms list
# 从 my-rpms repo 安装所有软件包
$ yum repo-pkgs my-rpms install
# 从 my-rpms 存储库中删除所有软件包
$ yum repo-pkgs my-rpms remove
```

#### makecache

下载 `yum` 存储库数据到缓存

### 故障排除和维护 YUM
<!--rehype:wrap-class=row-span-2-->

#### check

检查本地 RPM 数据库是否有问题（运行了很长时间）

#### history

```bash
# 列出所有 yum 安装、更新和清理操作
$ yum history list
# 显示 yum info 3 的详细信息
$ yum history info 3
# 撤消事务 3 中的 yum 操作
$ yum history undo 3
# 重做事务 3 中撤消的 yum 操作
$ yum history redo 3
```

#### clean

```bash
# 删除缓存中保存的包
$ yum clean packages
# 从缓存中清除所有包和元数据
$ yum clean all
```

清除缓存的包数据

#### fssnapshot

列出 LVM 快照（帮助在包更新后回滚）

#### fs

```bash
# 列出启用的文件系统过滤器
$ yum fs filters
# 过滤所有正在安装的文档（小心！）
$ yum fs documentation
```

对文件系统采取行动（防止在最小系统上安装 doc 或语言文件）非常有用！

### 使用 YUM 管理语言包

#### langavailable

列出已安装的语言 *

#### langinfo

```bash
# 列出与西班牙语相关的软件包
$ yum langinfo es
```

#### langinstall

```bash
# 安装与西班牙语相关的软件包
$ yum langinstall es
```

#### langlist

列出已安装的语言 *

#### langremove

```bash
# 删除与西班牙语相关的软件包
$ yum langremove es
```

### 使用 YUM 安装、删除和升级软件包
<!--rehype:wrap-class=row-span-2-->

#### install

```bash
# 安装 vsftpd 包
$ yum install vsftpd
```

#### update

```bash
# 使用可用更新更新所有软件包
$ yum update
# 更新 httpd 包（如果可用）
$ yum update httpd
# 应用与安全相关的包更新
$ yum update --security
```

#### update-to

将一个或所有软件包更新到特定版本

#### upgrade

```bash
$ yum -y upgrade
```

更新包考虑过时，只升级所有包，不升级软件和系统内核

#### localinstall

```bash
# 从本地文件、http 或 ftp 安装包
$ yum localinstall abc-1-1.i686.rpm
# 从本地目录安装 abc 包
$ yum localinstall http://myrepo/abc-1-1.i686.rpm
```
<!--rehype:className=wrap-text-->

从 FTP 站点安装 abc

#### downgrade

将软件包降级到早期版本

```bash
$ yum downgrade abc
```

将 abc 包降级到早期版本

#### reinstall

```bash
# 重新安装 util-linux（以替换任何已删除的文件）
$ yum reinstall util-linux
```

#### swap

```bash
# 删除 ftp 包并安装 lftp 包
$ yum swap ftp lftp
```

#### erase/remove

```bash
# 删除 vsftpd 包和依赖
$ yum remove vsftpd
```

#### autoremove

```bash
# 删除 httpd 和其他不需要的包
$ yum autoremove httpd
```

#### groupinstall

```bash
# 安装 Web 服务器包
$ yum groupinstall "Web server"
```

### 更多 YUM 相关命令（安装 yum-utils 软件包）

#### find-repos-of-install

查找包来自哪个存储库

#### needs-restarting

查找已更新且需要重启的进程

#### repoclosure

从存储库中获取未满足的依赖项列表

#### repoquery

查询远程仓库和本地 `RPM` 数据库

```bash
# 显示依赖包
$ repoquery --requires --resolve bash
```

#### reposync

将 `yum` 存储库同步到本地目录

```bash
# 从 repo 获取包
$ reposync -r rhel-atomic-host-beta-rpms
```

#### repotrack

下载一个包及其所有依赖项

#### show-installed

列出已安装的 RPM 包和统计信息

#### verifytree

检查本地 yum 存储库的一致性

#### yum-complete-transaction

尝试完成未完成的 yum 交易

#### yumdb

检查或更改 yum 数据库

#### yumdownloader

```bash
# 使用本地源离线安装 net-tools 工具包
$ yumdownloader net-tools.x86_64
# 使用 –destdir 参数设置下载的目标目录
$ yumdownloader net-tools.x86_64 --destdir=/usr/local/bin/
# 使用 –resolve 参数解决依赖关系并下载所需的安装包
$ yumdownloader net-tools.x86_64 --resolve --destdir=/usr/local/bin/
```
<!--rehype:className=wrap-text-->

从 repo 下载一个包到当前目录

### 不同 YUM 命令的常用选项

```bash
yum --disableplugin=langpacks info vsftpd
# 显示与正在运行的进程相关的包
yum --enableplugin=ps ps
yum install docker \
  --enablerepo=rhel-7-server-extras-rpm
yum list available --disablerepo=epel
# 下载 vsftpd 包到缓存
yum install --downloadonly vsftpd
```

----

:- | -
:- | -
`-y` | 如果出现提示，假设是
`--assumeno` | 如果提示，则假设否
`-q` | 不产生任何输出
`-v` | 产生额外的调试输出
`--noplugins` | 运行命令而不加载任何 yum 插件
`--disableplugin=` | 禁用单个命令的特定插件
`--enableplugin=` | 启用已安装但当前已禁用的插件
`--enablerepo=` | 为单个命令启用当前禁用的 repo（通配符可以）
`--disablerepo=` | 为单个命令禁用当前启用的 repo（通配符可以）
`--downloadonly` | 下载到 `/var/cache/yum/arch/prod/repo/packages/`，但不要安装
`--filter-???=` | 代替???与vendors, rpm-groups, arches 和其他人一起过滤输出
`--changelog` | 显示包的变更日志信息
<!--rehype:className=style-list-->

另见
---

- [YUM 官方网站](http://yum.baseurl.org/) _(yum.baseurl.org)_
- [YUM 备忘清单(适用于红帽 RedHat 企业 Linux)](https://access.redhat.com/sites/default/files/attachments/rh_yum_cheatsheet_1214_jcs_print-1.pdf) _(access.redhat.com)_
- [用 yum 管理软件包](http://prefetch.net/articles/yum.html) _(prefetch.net)_
- [Fedora 中的 Yum 文档](https://docs.fedoraproject.org/en-US/Fedora/15/html/Deployment_Guide/ch-yum.html) _(fedoraproject.org)_
- [CentOS 中的 Yum 文档](http://wiki.centos.org/PackageManagement/Yum/) _(wiki.centos.org)_
- [Scientific Linux 中的 Yum 文档](https://www.scientificlinux.org/documentation/faq/yum.apt.repo) _(scientificlinux.org)_


APT 清单查询
---

### 介绍
<!--rehype:wrap-class=row-span-2-->
APT（`A`dvanced `P`ackaging `T`ools）是`Debian`及其派生的`Linux`软件包管理器。APT可以自动下载，配置，安装二进制或者源代码格式的软件包，因此简化了Unix系统上管理软件的过程。APT最早被设计成`dpkg的前端`，用来处理deb格式的软件包。现在经过`APT-RPM`组织修改，APT已经可以安装在支持RPM的系统管理RPM包。

它结合了apt-get和apt-cache工具中最常用的命令以及选项与默认值。`apt`命令必须以具有`sudo`权限的用户运行。

命令语法格式

```bash
$ apt [ OPTIONS ] COMMAND
```

----

相关参考文献

- [APT（8） 官方网站](https://manpages.debian.org/unstable/apt/apt.8.en.html)
- [apt.conf(5) 官方文档](https://manpages.debian.org/unstable/apt/apt.conf.5.en.html)
- [sources.list(5) 官方文档](https://manpages.debian.org/unstable/apt/sources.list.5.en.html)

### 命令查询

子命令描述和任务，显示 apt 命令和选项。

```bash
$ apt -h or --help
# 或
$ apt 
```

查看指令用法

```bash
$ man apt
```

### update

从APT存储库中获取最新索引数据。

```bash
$ sudo apt update
```

在升级或安装新软件包之前，建议始终先运行一次更新软件包索引。

### upgrade

将安装的软件包升级到最新版本，该命令不会升级那些已删除软件包的依赖。

```bash
$ sudo apt upgrade
```

升级单个软件包。

```bash
$ sudo apt upgrade package_name
```

升级整个系统，则会删除当前安装的软件包。

```bash
$ sudo apt full-upgrade
```

### install

安装软件包。

```bash
$ sudo apt install package_name
```

如果只想升级，不要安装

```bash
$ sudo apt install <package_name> --only-upgrade
```
<!--rehype:className=wrap-text -->

安装多个软件包，包名用空格分隔。

```bash
$ sudo apt install package1 package2
```

安装本地deb文件，提供文件的完整路径。否则，apt命令将尝试从APT存储库中检索并安装软件包。
`Deb是所有基于Debian的发行版使用的安装软件包格式`。

```bash
$ sudo apt install /full/path/file.deb
```

### remove和purge
<!--rehype:wrap-class=row-span-2-->

要删除已安装的程序包，你可以使用apt子命令`remove`和`purge`。

#### remove

remove子命令将卸载指定的软件包，`但可能会留下一些配置文件`。
通过remove方式卸载的软件包可以通过重新安装软件包来恢复，因为个人配置文件还在本地。

卸载指定的软件包

```bash
$ sudo apt remove package_name
```

指定多个软件包，以空格分隔

```bash
$ sudo apt remove package1 package2
```

#### purge

purge子命令将卸载指定的软件包和配置文件。

```bash
$ sudo apt purge package_name
```

### autoremove自动删除依赖

用于删除自动安装的包，这些包都是为了满足其他包的依赖关系，现在不再需要这些包，因为依赖关系已更改或者同时删除了需要它们的包。

```bash
$ sudo apt autoremove
```

### list
<!--rehype:wrap-class=row-span-2-->

打印所有软件包的列表，包括软件包的版本和结构的信息。

```bash
$ sudo apt list
```

要确定是否安装了指定的软件包，可以使用grep命令过滤输出。

```bash
$ sudo apt list | grep package_name
```

仅列出已安装的软件包。

```bash
$ sudo apt list --installed
```

获取可升级软件包的列表。

```bash
$ sudo apt list --upgradeable
```

### 搜索查找软件包详细信息

#### search

在可用软件源列表中搜索指定的软件包。如果找到该软件包，则将返回名称与搜索词匹配的软件包。

```bash
$ sudo apt search package_name
```

#### show

显示有关给定软件包的信息，包括其依赖项、安装、下载大小、软件包可用的来源、软件包内容的描述等。

```bash
$ sudo apt show package_name
```

### edit-sources 快速换源

允许您在首选的文本编辑器中编辑`sources.list(5)` 文件，同时还提供基本的健全性检查。

首次换源可以使用`edit-sources`

```bash
$ sudo apt show edit-sources
```

换源后更新一下软件包索引。

```bash
$ sudo apt update
```

之后可以使用`select-editor`更换默认编辑器

```bash
$ sudo select-editor
```
