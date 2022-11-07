---
cover: >-
  https://images.unsplash.com/photo-1665606133288-10784ac63596?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHJhbmRvbXx8fHx8fHx8fDE2Njc1NzM0NzI&ixlib=rb-4.0.3&q=80
coverY: 0
---

# Linux 安装 Mysql

## 下载

去官网 [_MySQL Product Archives_](https://downloads.mysql.com/archives/community/) 下载相关版本 `Mysql` 安装介质

本文所使用 _Mysql 5.7.37：_ `mysql-5.7.37-linux-glibc2.12-x86_64.tar.gz` 进行安装

## 准备工作

* 检查是否已安装 `Mysql`

> 使用以下命令
>
> `rpm -qa | grep mysql`

```shell
[root@arise hfins]# rpm -qa | grep mysql
[root@arise hfins]# 
```

_「 Tips：若已经安装过其他版本 `Mysql`，可通过 `rpm -e 已经存在的Mysql全名` 命令进行卸载 」_

* 添加用户组

> 当前用户组用于管理 `Mysql`，以提高安全性「非必须，可选」
>
> `groupadd mysql` `useradd -r -g mysql -s /bin/false mysql`

```shell
[root@arise hfins]# groupadd mysql
[root@arise hfins]# useradd -r -g mysql -s /bin/false mysql
```

* 安装 `libaio-devel`

> `libaio-devel` 为 `Mysql` 必须的安装依赖，需提前安装
>
> `yum install libaio-devel.x86_64`

```shell
[root@arise hfins]# yum install libaio-devel.x86_64
Loaded plugins: fastestmirror, product-id, search-disabled-repos, subscription-manager

This system is not registered with an entitlement server. You can use subscription-manager to register.

Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
base                                                                                                                                                                                                                         | 3.6 kB  00:00:00     
extras                                                                                                                                                                                                                       | 2.9 kB  00:00:00     
updates                                                                                                                                                                                                                      | 2.9 kB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package libaio-devel.x86_64 0:0.3.109-13.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

====================================================================================================================================================================================================================================================
 Package                                                       Arch                                                    Version                                                          Repository                                             Size
====================================================================================================================================================================================================================================================
Installing:
 libaio-devel                                                  x86_64                                                  0.3.109-13.el7                                                   base                                                   13 k

Transaction Summary
====================================================================================================================================================================================================================================================
Install  1 Package

Total download size: 13 k
Installed size: 7.8 k
Is this ok [y/d/N]: y
Downloading packages:
libaio-devel-0.3.109-13.el7.x86_64.rpm                                                                                                                                                                                       |  13 kB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : libaio-devel-0.3.109-13.el7.x86_64                                                                                                                                                                                               1/1 
  Verifying  : libaio-devel-0.3.109-13.el7.x86_64                                                                                                                                                                                               1/1 

Installed:
  libaio-devel.x86_64 0:0.3.109-13.el7                                                                                                                                                                                                              

Complete!
[root@arise hfins]# 
```

## 安装

* 解压 `mysql-5.7.37-linux-glibc2.12-x86_64.tar.gz` 至需要安装的目录

> 使用如下命令，将 `Mysql` 解压至
>
> `tar -xvf mysql-5.7.37-linux-glibc2.12-x86_64.tar.gz -C /usr/local`

```shell
[root@arise hfins]# tar -xvf mysql-5.7.37-linux-glibc2.12-x86_64.tar.gz -C /usr/local
mysql-5.7.37-linux-glibc2.12-x86_64/bin/myisam_ftdump
mysql-5.7.37-linux-glibc2.12-x86_64/bin/myisamchk
mysql-5.7.37-linux-glibc2.12-x86_64/bin/myisamlog
mysql-5.7.37-linux-glibc2.12-x86_64/bin/myisampack
mysql-5.7.37-linux-glibc2.12-x86_64/bin/mysql
mysql-5.7.37-linux-glibc2.12-x86_64/bin/mysql_client_test_embedded
mysql-5.7.37-linux-glibc2.12-x86_64/bin/mysql_config_editor
mysql-5.7.37-linux-glibc2.12-x86_64/bin/mysql_embedded
...
[root@arise hfins]#
```

> 更改安装目录至 `mysql`
>
> `mv mysql-5.7.37-linux-glibc2.12-x86_64 /usr/local/mysql`

```shell
[root@arise local]# mv mysql-5.7.37-linux-glibc2.12-x86_64/ /usr/local/mysql
[root@hfinsrdproddb local]# ll
total 0
drwxr-xr-x. 2 root root  28 Apr 11  2018 bin
drwxr-xr-x. 2 root root   6 Apr 11  2018 etc
drwxr-xr-x. 2 root root   6 Apr 11  2018 games
drwxr-xr-x. 2 root root   6 Apr 11  2018 include
drwxr-xr-x. 2 root root   6 Apr 11  2018 lib
drwxr-xr-x. 2 root root   6 Apr 11  2018 lib64
drwxr-xr-x. 2 root root   6 Apr 11  2018 libexec
drwxr-x---  9 root root 129 Jul 17 20:57 mysql
drwxr-xr-x. 2 root root   6 Apr 11  2018 sbin
drwxr-xr-x. 5 root root  49 Apr 11  2018 share
drwxr-xr-x. 2 root root   6 Apr 11  2018 src
[root@arise local]# 
```

> 授权
>
> `chown -R mysql:mysql mysql`

```shell
[root@arise local]# chown -R mysql:mysql mysql
[root@arise local]# 
```

## 配置

* 配置 `Mysql` 服务

> 将 `support-files` 目录下的 `mysql.server` 复制到 `/etc/init.d/` 并重命名为 `mysql`
>
> `cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql`

```shell
[root@arise local]# cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql
[root@hfinsrdproddb local]# cd /etc/init.d/
[root@hfinsrdproddb init.d]# ll
total 56
-rwxr-xr-x 1 root root  2531 Jan 15  2020 filebeat
-rw-r--r-- 1 root root 18281 May 22  2020 functions
-rwxr-x--- 1 root root 10576 Jul 17 21:05 mysql
-rwxr-xr-x 1 root root  4569 May 22  2020 netconsole
-rwxr-xr-x 1 root root  7928 May 22  2020 network
-rw-r--r-- 1 root root  1160 Jan 14  2022 README
[root@arise init.d]# 
```

* 调整 `/etc/init.d/mysql` 参数

> 指定 `basedir` 及 `datadir` 目录
>
> `vim /etc/init.d/mysql`
>
> 配置以下内容
>
> `basedir=/usr/local/mysql` `datadir=/usr/local/mysql/data`
>
> _「 Tips：`datadir` 目录请以实际需存放 `mysql` 数据文件要求为准，本文档设置到 `mysql` 安装目录」_

```shell
[root@arise init.d]# vim /etc/init.d/mysql
#!/bin/sh
# Copyright Abandoned 1996 TCX DataKonsult AB & Monty Program KB & Detron HB
# This file is public domain and comes with NO WARRANTY of any kind

# MySQL daemon start/stop script.

# Usually this is put in /etc/init.d (at least on machines SYSV R4 based
# systems) and linked to /etc/rc3.d/S99mysql and /etc/rc0.d/K01mysql.
# When this is done the mysql server will be started when the machine is
# started and shut down when the systems goes down.

# Comments to support chkconfig on RedHat Linux
# chkconfig: 2345 64 36
# description: A very fast and reliable SQL database engine.

# Comments to support LSB init script conventions
### BEGIN INIT INFO
# Provides: mysql
# Required-Start: $local_fs $network $remote_fs
# Should-Start: ypbind nscd ldap ntpd xntpd
# Required-Stop: $local_fs $network $remote_fs
# Default-Start:  2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: start and stop MySQL
# Description: MySQL is a very fast and reliable SQL database engine.
### END INIT INFO

# If you install MySQL on some other places than /usr/local/mysql, then you
# have to do one of the following things for this script to work:
#
# - Run this script from within the MySQL installation directory
# - Create a /etc/my.cnf file with the following information:
#   [mysqld]
#   basedir=<path-to-mysql-installation-directory>
# - Add the above to any other configuration file (for example ~/.my.ini)
#   and copy my_print_defaults to /usr/bin
# - Add the path to the mysql-installation-directory to the basedir variable
#   below.
#
# If you want to affect other MySQL variables, you should make your changes
# in the /etc/my.cnf, ~/.my.cnf or other MySQL configuration files.

# If you change base dir, you must also change datadir. These may get
# overwritten by settings in the MySQL configuration files.

basedir=/usr/local/mysql
datadir=/usr/local/mysql/data
```

* 配置 `Mysql` 文件

> 由于本次安装的 `5.7.37` 版本 `mysql` 的 `support-files` 目录中没有默认配置文件，需自己准备；以下提供可参考的基础配置
>
> 于 `/etc/` 目录下新建 `my.cnf` 文件
>
> _「 Tips： 1、其他版本 `mysql` 若有 `my.cnf` 文件则直接参考基础配置进行修改即可； 2、在 `/etc/` 目录下可能已经存在 `my.cnf` 文件，这是默认安装的数据库配置文件，直接用基础配置内容覆盖即可; 3、需检查 `my.cnf` 目录下是否一并存在 `my.cnf.d` 文件夹，否则安装时会报错 」_
>
> `touch /etc/my.cnf` _「 Tips：若已经存在该文件则不需要重新创建 」_ `vim /etc/my.cnf`

```shell
# *** DO NOT EDIT THIS FILE. It's a template which will be copied to the
# *** default location during install, and will be replaced if you
# *** upgrade to a newer version of MySQL.
[client]
port = 3306
socket=/var/lib/mysql/mysql.sock

# 普通项目的编码方式可以设置成 utf8
# 这里设置成utf8mb4，是因为我的项目需要存储 emoji 表情，
# 这种表情虽然是utf8编码，但是一个字符需要占用4个字节，而 MySQL utf8编码只能存放3字节的字符。
# 在 MySQL 5.6 以上版本中，可以设置编码为utf8mb4，这个字符集是utf8的超集。
default-character-set=utf8mb4

[mysqld]
# 一般配置选项
basedir = /usr/local/mysql
datadir = /hfins/mysql/data
port = 3306
character-set-server=utf8mb4
default_storage_engine = InnoDB
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
socket=/var/lib/mysql/mysql.sock

# 设置最大连接数
max_connections=2048

# 下面一行是忽略大小写的配置，不想忽略的话可以删除，或者把值改成 0;
lower_case_table_names=1

# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0
# Settings user and group are ignored when systemd is used.
# If you need to run mysqld under a different user or group,
# customize your systemd unit file for mariadb according to the

[mysqld_safe]
log-error=/var/log/mysql/mariadb/mariadb.log
pid-file=/var/run/mysql/mariadb/mariadb.pid

#
# include all files from the config directory
#
!includedir /etc/my.cnf.d
```

* 创建目录文件及授权

> 配置文件中设置很多默认的文件及目录，需进行提前创建及授权
>
> `mariadb` 目录及日志文件
>
> `mkdir -p /var/log/mysql/mariadb` `touch /var/log/mysql/mariadb/mariadb.log` `chown -R mysql:mysql /var/log/mysql`
>
> `run` 目录
>
> `mkdir /var/run/mysql` `chown -R mysql:mysql /var/run/mysql`
>
> `lib` 目录及创建软链
>
> `mkdir /var/lib/mysql` `chown -R mysql:mysql /var/lib/mysql` `ln -s /var/lib/mysql/mysql.sock /tmp/mysql.sock`

```shell
[root@arise etc]# mkdir -p /var/log/mysql/mariadb
[root@arise etc]# touch /var/log/mysql/mariadb/mariadb.log
[root@arise etc]# chown -R mysql:mysql /var/log/mysql
[root@arise etc]# mkdir /var/run/mysql
[root@arise etc]# chown -R mysql:mysql /var/run/mysql
[root@arise etc]# mkdir /var/lib/mysql
[root@arise etc]# chown -R mysql:mysql /var/lib/mysql
[root@arise etc]# ln -s /var/lib/mysql/mysql.sock /tmp/mysql.sock
[root@arise etc]# 
```

* 初始化数据库

> 切换到 `mysql` 的 `bin` 目录执行以下命令
>
> `./mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data`
>
> _「 Tips： 1、`datadir` 目录请以实际需存放 `mysql` 数据文件要求为准，本文档设置到 `mysql` 安装目录 2、执行完成后，末尾会打印出默认生成的初始密码，请注意备份 」_

```shell
[root@arise bin]# ./mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
2022-07-17T13:45:54.307123Z 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
2022-07-17T13:45:54.844094Z 0 [Warning] InnoDB: New log files created, LSN=45790
2022-07-17T13:45:54.923713Z 0 [Warning] InnoDB: Creating foreign key constraint system tables.
2022-07-17T13:45:54.986564Z 0 [Warning] No existing UUID has been found, so we assume that this is the first time that this server has been started. Generating a new UUID: c7b29dc7-05d6-11ed-8cbd-72faf2c87225.
2022-07-17T13:45:54.988120Z 0 [Warning] Gtid table is not ready to be used. Table 'mysql.gtid_executed' cannot be opened.
2022-07-17T13:45:55.811831Z 0 [Warning] A deprecated TLS version TLSv1 is enabled. Please use TLSv1.2 or higher.
2022-07-17T13:45:55.811867Z 0 [Warning] A deprecated TLS version TLSv1.1 is enabled. Please use TLSv1.2 or higher.
2022-07-17T13:45:55.813011Z 0 [Warning] CA certificate ca.pem is self signed.
2022-07-17T13:45:55.913845Z 1 [Note] A temporary password is generated for root@localhost: MeuyTpuLK1(O
```

* 配置环境变量

> 初始化完成后，需设置 `mysql` 环境变量；进入 `/etc/profile.d` 目录创建 `mysql.sh` 文件
>
> 创建 `mysql.sh`文件
>
> `cd /etc/profile.d` `touch mysql.sh`
>
> 编辑 `mysql.sh` 文件
>
> `vim mysql.sh`

```shell
# Mysql 环境变量设置
MYSQL_HOME=/usr/local/mysql
PATH=$PATH:$MYSQL_HOME/bin
export MYSQL_HOME PATH
```

> 立即生效
>
> `source /etc/profile`

```shell
[root@arise bin]# cd /etc/profile.d
[root@arise profile.d]# touch mysql.sh
[root@arise profile.d]# vim mysql.sh
# Mysql 环境变量设置
MYSQL_HOME=/usr/local/mysql
PATH=$PATH:$MYSQL_HOME/bin
export MYSQL_HOME PATH
[root@arise profile.d]# source /etc/profile
[root@arise profile.d]# 
```

## 启动

> 使用以下命令，启动 `mysql`
>
> `service mysql start`

```shell
[root@arise ~]# service mysql start
Starting MySQL. SUCCESS! 
[root@arise ~]# 
```

## 停止

> 使用以下命令，停止 `mysql`
>
> `service mysql stop`

```shell
[root@arise ~]# service mysql stop
Shutting down MySQL.. SUCCESS! 
[root@arise ~]# 
```

## 登录

* 登录

> 使用以下命令，登录 `mysql`；需输入初始化数据库时默认生成的 `root` 密码
>
> `mysql -uroot -p`

```shell
[root@arise ~]# mysql -uroot -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.37

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

* 修改密码

> 若需要调整 `root` 密码，可在登录后使用以下命令
>
> `set password=password('新密码')`

```shell
mysql> set password=password('xxxxxx');
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> 
```

## 开启远程登录

> 在登录后使用以下命令，设置 `mysql` 远程登录
>
> 授权
>
> `grant all privileges on *.* to root@'%' identified by 'root密码';`
>
> 刷新权限
>
> `flush privileges;`

```shell
mysql> grant all privileges on *.* to root@'%' identified by 'xxxxxx';
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)

mysql> 
```

> 若服务器启用防火墙，还需开放 `3306` 端口；可参考防火墙设置篇 [_CentOS 7 防火墙_](https://note.youdao.com/s/1sA43Cmo)

* 设置开机自启

> 使用以下命令，设置 `mysql` 开机自动启动
>
> 查看自启服务列表
>
> `chkconfig --list`
>
> 添加 `mysql`
>
> `chkconfig --add mysql`
>
> 开启自启动
>
> `chkconfig mysql on`

```shell
[root@arise ~]# chkconfig --list

Note: This output shows SysV services only and does not include native
      systemd services. SysV configuration data might be overridden by native
      systemd configuration.

      If you want to list systemd services use 'systemctl list-unit-files'.
      To see services enabled on particular target use
      'systemctl list-dependencies [target]'.

netconsole      0:off   1:off   2:off   3:off   4:off   5:off   6:off
network         0:off   1:off   2:on    3:on    4:on    5:on    6:off
[root@arise ~]# chkconfig --add mysql
[root@arise ~]# chkconfig mysql on
[root@arise ~]# chkconfig --list

Note: This output shows SysV services only and does not include native
      systemd services. SysV configuration data might be overridden by native
      systemd configuration.

      If you want to list systemd services use 'systemctl list-unit-files'.
      To see services enabled on particular target use
      'systemctl list-dependencies [target]'.

mysql           0:off   1:off   2:on    3:on    4:on    5:on    6:off
netconsole      0:off   1:off   2:off   3:off   4:off   5:off   6:off
network         0:off   1:off   2:on    3:on    4:on    5:on    6:off
[root@arise ~]# 
```

_「 Tips：设置 `mysql` 开机自启后，`chkconfig --list` 可查看到 `mysql` 2\~5 都显示 `on` 状态 」_

* 参考文献

***

`[ 1 ]`[ `MySQL 5.7 Reference Manual`](https://dev.mysql.com/doc/refman/5.7/en/)
