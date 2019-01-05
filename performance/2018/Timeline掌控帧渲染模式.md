---
layout: page
title: Timeline 掌控帧渲染模式
permalink: /performance/2018_10_20
---

### Timeline 掌控帧渲染模式

#### 基本知识

- 网页动画能够做到每秒 60 帧，就会跟显示器同步刷新，一秒之内进行 60 次重新渲染，每次重新渲染的时间不能超过 16.66 毫秒
- 蓝色：网络通信和 HTML 解析
- 黄色：JavaScript 执行
- 紫色：样式计算和布局，即重排
- 绿色：重绘
- window.requestAnimationFrame() 下一次重新渲染
- window.requestIdleCallback() 下几次重新渲染

#### 触发分层

- 获取 DOM 并将其分割为多个层

  - DOM 子树渲染层（RenderLayer）-> RenderObject -> GraphicsContext(根元素、position、transform、半透明、CSS 滤镜、Canvas2D、video、溢出)
  - Compositor -> 渲染层子树的图形层(GraphicsLayer) -> RenderLayer -> RenderObject
  - Compositor 将所有的拥有 compositing layer 进行合成，合成过程 GUP 进行参与。合成完毕就能够将纹理映射到一个网格几何结构之上 - 在视频游戏或者 CAD 程序中，这种技术用来给框架式的 3D 模型添加“皮肤”。Chorme 采用纹理把页面中的内容分块发送给 GPU。纹理能够以很低的代价映射到不同的位置，而且还能够以很低的代价通过把它们应用到一个非常简单的矩形网格中进行编写。这就是 3D CSS 的实现原理。（CSS3D 透视变换、video、webgl、transform 动画、加速 CSS 滤镜。叠加在已经触发合成层）

- 将每个层独立的绘制进位图中
- 将层作为纹理上传至 GPU
- 复合多个层来生成最终的屏幕图像

#### 如何开发不会导致重排

- 样式表越简单，重排和重绘就越快
- 重排和重绘的 DOM 元素层级越高，成本就越高
- table 元素的重排和重绘成本，要高于 div 元素
- 尽量不要把读操作和写操作，放在一个语句里面
- 统一改变样式
- 缓存重排结果
- 离线 DOM Fragment/clone
- 虚拟 DOM React
- 必要的时候 display: none 不可见元素不影响重排重绘。visibility 对重排影响不影响重绘

> 网页生成的时候，至少会渲染一次。用户访问的过程中还会不断重新渲染。以下三种情况，会导致网页重新渲染。
>
> 1. 修改 DOM
> 2. 修改样式表
> 3. 用户事件
>
> 重新渲染，就需要重新生成布局和重新绘制。前者叫做“重排”（reflow），后者叫做“重绘”（repaint）
> 需要注意的是，“重绘”不一定需要“重排”，比如改变某个网页元素的颜色，就只会触发“重绘”，不会触发“重排”，因为布局没有改变。但是“重排”必然导致“重绘”，比如改变一个网页元素的位置，就会同事触发“重绘”和“重排”，因为布局改变了。
