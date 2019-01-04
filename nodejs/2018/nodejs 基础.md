---
layout: page
title: nodejs 基础
permalink: /nodejs/2018_10_8
---

### nodejs 基础

#### 事件驱动模型（事件驱动 IO 模型、非阻塞式 IO）

![事件驱动模型]({{ site.baseurl }}/{{ site.assets }}/event_loop.png)

```
<!-- 1. 引入Event模块，并创建eventsEmitter对象 -->
var events = require('events);
var eventEmitter = new events.EventEmitter();

<!-- 绑定事件处理函数 -->
eventEmitter.on('connection', function(){
    // to do something
})

<!-- 触发事件 -->
eventEmitter.emit();
```

#### node.js 的模块加载流程

- nodejs 中存在 4 类模块（原生模块和三种文件模块）
  ![模块加载流程]({{ site.baseurl }}/{{ site.assets }}/require.png)
  
- 文件模块缓存区，原生模块缓存区
  - 从文件模块加载
  - 从原生模块加载
  - 从文件加载

- require 方法加载模块
  - http、fs、path 等，原生模块
  - ./mod, ../mod, 相对路径的文件模块
  - /root/mod, 绝对路径的文件模块
  - mod， 非原生模块的文件模块

#### node.js 热重启工具

- supervisor app.js

#### 爬虫

- 是一种自动获取网页内容的程序。是搜索引擎的重要组成部分，因此搜索引擎很大程度上是针对爬虫而做出的优化。

- robots.txt 是一个文本文件，robots.txt 是一个协议，不是一个命令。robots.txt 是爬虫要查看的第一个文件。robots.txt 文件告诉爬虫在服务器上什么文件是可以被查看的，搜索机器人就会按照该文件中的内容来确定访问的范围。

#### comet(http 长连接)

- 后端推送的方式
- 前端轮询的方式

#### 数据推送之 sse (Server-Send Event)

- EventSource
