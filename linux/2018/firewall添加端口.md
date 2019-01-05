---
layout: page
title: firewall添加端口
permalink: /linux/2018_11_10
---

### firewall添加端口

#### 永久添加 443 端口
```
$ firewall-cmd --zone=public --add-port=3000/tcp --permanent
```

#### 重载端口
```
$ firewall-cmd --reload
```

#### 查看防火墙规则
```
$ firewall-cmd --list-all
```