---
layout: page
title: Google AMP
permalink: /performance/2018_10_19
---

### Google AMP

> AMP 是一个开放源代码库，它提供了一种非常简单的方法，让您能够轻松地为用户创建富有吸引力、运行顺畅且几乎可即时完成加载的网页。AMP 网页其实只是可由您链接到和控制的网页而已。

#### 三大构成

- AMP HTML: 是为确保实现可靠性能而设有一些限制的 HTML。

```
<!doctype html>
<html>
 <head>
   <meta charset="utf-8">
   <link rel="canonical" href="hello-world.html">
   <meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">
   <style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}</style><noscript><style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style></noscript>
   <script async src="https://cdn.ampproject.org/v0.js"></script>
 </head>
 <body>Hello World!</body>
</html>
```

- AMP JS: 可确保 AMP HTML 网页快速呈现。

  - AMP JS 库可实现 所有 AMP 最佳性能做法、 管理资源加载并为您提供上述自定义标记， 所有这一切都是为了确保您的网页能够快速呈现。
  - 最重大的优化措施之一是，AMP 可使来自外部资源的所有内容异步加载，让网页中的任何内容都能顺畅无碍地呈现。
  - 其他的性能提升技术包括：将所有 iframe 沙盒化、在加载资源之前预先计算网页上各元素的布局，以及停用运行缓慢的 CSS 选择器。

- AMP 缓存: 可用于提供缓存的 AMP HTML 网页。
  - Google AMP 缓存是一种基于代理的内容传送网络， 用于传送所有有效的 AMP 文档。
  - 它可提取和缓存 AMP HTML 网页，并自动改进网页性能。
  - 在使用 Google AMP 缓存时，相应文档、所有 JS 文件以及所有图片都会 从同一个使用 HTTP 2.0 的来源加载，以实现最高效率。

#### 参考

- [Google AMP](https://www.ampproject.org/zh_cn/)
