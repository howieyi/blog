---
layout: page
title: 修改 hostname
permalink: /linux/2018_3_29
---

### 修改 hostname

#### 查看当前主机名
```
$ hostname
```

#### 修改hostname
- readhat/centos/fedora
```
$ vi /etc/sysconfig/network
```
- debian/ubuntu
```
$ vi /etc/hostname
```

#### 后续操作
```
// 输入新hostname 并保存  
$> HOSTNAME=newname
// 保存后执行
$ hostname newname
$ hostname
```

