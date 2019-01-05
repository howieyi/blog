---
layout: page
title: Ubuntu 虚拟机无法打开锁文件
permalink: /linux/2018_1_23
---

### Ubuntu 虚拟机无法打开锁文件

#### 方法一
```
$ sudo dbkg --configure -a
```

#### 方法二
```
$ sudo rm /var/lib/apt/lists/lock
```


