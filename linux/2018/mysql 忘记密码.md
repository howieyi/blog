---
layout: page
title: mysql 忘记密码
permalink: /linux/2018_3_25
---

### mysql 忘记密码

#### 关闭数据库
```
$ service mysqld stop (centos)
$ mysql.server stop (mac)
```

#### 使用 “--skip-grant-tables”参数重新启动mysql
```
$ mysqld_safe --skip-grant-tables &
```

#### 用帐号登录mysql(这个时候任意密码可登陆)
```
$ mysql -u root -p
```

#### 改变用户数据库，修改密码
```
$ mysql> use mysql;
$ mysql> update user set password=password('admin123') where user='root';
$ mysql> flush previleges;
$ mysql> quit;
```

#### 重启mysql
```
$ service mysqld restart (centos)
$ mysql.server restart (mac)
```