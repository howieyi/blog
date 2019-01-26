---
layout: page
title: 高性能JavaScript - 加载与执行
permalink: /performance/2019_01_26
---

### 高性能JavaScript - 加载与执行

在浏览器加载JavaScript的过程中，浏览器必须花时间下载外链文件中的代码，然后解析并执行。在这个过程中，页面渲染和用户交互是完全被阻塞的。

#### 优化注意事项

- 引用
  - 样式前置，在`head`中引入`style`或者`link src`
  - `script`脚本后置，`</body>`闭合标签之前，避免阻塞页面渲染
  - 合并脚本，减少页面中外链的脚本文件的数量（考虑到HTTP请求带来的性能开销，下载单个100KB的文件将比下载4个25KB的文件更快）

- 异步加载
  - 无阻塞式脚本，页面加载完成后再加载JavaScript，即`window.onload`事件触发后再下载脚本
  - 延迟的脚本，采用`script`扩展属性，`defer`（需要等待页面完成后执行），`async`（加载完成后自动执行）均是采用并行下载，`defer`属性的script标签可以放置在任何位置，页面解析到时候开始加载，但是并不执行，直到DOM加载完成（onload事件触发之前）
  - 动态脚本，采用`createElement('script')`创建，使用`appendChild`添加到`head`中
  - `XMLHttpRequest`脚本注入，通过HTTP请求方式加载脚本
  - 第三方异步加载库...