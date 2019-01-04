---
layout: page
title: HTML 标签的巧妙运用
permalink: /html/2018_8_6
---

### HTML 标签的巧妙运用

#### img 的使用

- Image onload 计算网速
- 通过小图访问记录用户行为（原理：通过 web 服务的 access 日志分析用户行为数据)

```
https://hm.baidu.com/hm.gif?cc=0&ck=1&cl=24-bit&ds=375x667&vl=667&et=0&ja=0&ln=zh-cn&lo=0&rnd=342377793&si=12423ecbc0e2ca965d84259063d35238&v=1.2.33&lv=1&ct=!!&tt=%E7%99%BE%E5%BA%A6%E4%B8%80%E4%B8%8B&sn=52245
```

- img 的 crossOrigin 属性（针对 canvas 绘制的同源策略，绘制跨域图片将导致画布污染，无法预览跨域图片，例如将不能使用 canvas 的 toBlob(), toDataURL(), getImageData() 方法，调用它们会抛出安全错误。设置 crossOrigin="Anonymous" 可配合 web 服务设置 cros 来避免污染 canvas 绘制，使得图片可以绘制，）

#### navigator.sendBeacon(url[, data(将要发送的 ArrayBufferView, Blob, DOMString, 或者 FormData 类型的数据。)]) (实验中的功能)

- 可用于通过 HTTP 将少量数据异步传输到 Web 服务器，主要用于满足 统计和诊断代码 的需要，这些代码通常尝试在卸载（unload）文档之前向 web 服务器发送数据。
- 使用 sendBeacon() 方法，将会使用户代理在有机会时异步地向服务器发送数据，同时不会延迟页面的卸载或影响下一导航的载入性能。

```
window.addEventListener('unload', logData, false);

function logData() {
    navigator.sendBeacon("/log", analyticsData);
}
```

#### xss 注入漏洞

- css 中 url 属性，可跨域，并可注入 js 代码
- src 属性的远程脚本注入，iframe、link、script、img、video、audio、embed 等等标签
- href 属性，例如 href="javascript:....."

#### html 语义化的重要性

- 针对 seo 友好，使得浏览器更容易识别每个 dom 模块的存在意义

#### iframe 扩容 localStorage

- A: window.frames[0].postMessage(data, 'http://localhost:85')
- B: window.addEventListener('message', function(e){}, false);
- window.postMessage() 方法可以安全地实现跨源通信。通常，对于两个不同页面的脚本，只有当执行它们的页面位于具有相同的协议（通常为 https），端口号（443 为 https 的默认值），以及主机 (两个页面的模数 Document.domain 设置为相同的值) 时，这两个脚本才能相互通信。window.postMessage() 方法提供了一种受控机制来规避此限制，只要正确的使用，这种方法就很安全。
