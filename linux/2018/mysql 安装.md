---
layout: page
title: mysql 安装
permalink: /linux/2018_3_5
---

### mysql 安装

#### mac 安装(brew)
- 安装
```
$ brew update
$ brew install mariadb
```
- 更新
```
$ brew upgrade mariadb
```
- 启动
```
$ mysql.server start
```
- 自启动
```
$ brew services start mariadb
```
- mysql 脚本
```
mysql -u root
```

#### centos 安装
- [参考1](https://linux.cn/article-8320-1.html)
- [参考2](https://mariadb.com/kb/en/library/yum/)
- 添加yum仓库
```
$ vi /etc/yum.repos.d/MariaDB.repo
```    

```
[mariadb] 
name  =  MariaDB 
baseurl  =  http://yum.mariadb.org/10.1/centos7-amd64 
gpgkey = https://yum.mariadb.org/RPM-GPG-KEY-MariaDB 
gpgcheck = 1
```

- 安装
```
$ yum install MariaDB-server MariaDB-client
```

- 启动MariaDB
```
$ systemctl start mariadb
$ systemctl enable mariadb
$ systemctl status mariadb
```

- 设置密码以及其他相关配置
```
$ mysql_secure_installation
```