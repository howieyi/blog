---
layout: page
title: a 标签容易忽略的安全问题
permalink: /html/2019_1_10
---

## a 标签容易忽略的安全问题

### `target="_blank"`打开的新tab
- 与原始页面同一进程和线程中启动的窗口
- 新页面有任何性能上的问题，比如有一个很高的加载时间，这也将会影响到原始页面的表现
- 你打开的是一个同域的页面，那么你将可以在新页面访问到原始页面的所有内容，包括`document`对象。(`window.opener.document`)
- 如果你打开的是一个跨域的页面，你虽然无法访问到document，但是你依然可以访问到`location`对象。

### 解决办法
#### 标签 `rel="noopener"`
- `rel="noopener"` 防止 `window.opener`，因此没有跨窗口访问
```
<a href="https://examplepetstore.com" target="_blank" rel="noopener">...</a>
```

#### JavaScript中
```
var newWindow = window.open();
newWindow.opener = null;
```
