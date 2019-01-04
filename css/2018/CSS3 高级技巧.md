---
layout: page
title: CSS3 高级技巧
permalink: /css/2018_8_11
---

### CSS3 高级技巧

#### 双飞翼布局

- position
- float
- 负边距
- 等高
- 盒子模型
- 清除浮动

#### 基于移动端的 px 与 rem 转换兼容方案

- different size different DPR
- 目前的设计稿 一般是 640 750 1125，一般要先均分成 100 份，(兼容 vh,vm) 750/10 = 75px。div 宽是 240px*120px css 的书写改为 3.2rem * 1.6rem。 配合响应式修改 html 根的大小。
- 字体不建议使用 rem 的，data-dpr 属性动态设置字体大小。屏幕变大放更多的文字，或者屏幕更大放更多的字。
- 神奇的 padding/margin-top 等比例缩放间距

#### 弹性盒模型与 Reset 的选择

- `flex` 模型，兼容性已经很好，移动端基本通用
- `*`的杀伤力太大，慎用
- `Reset.css`重置，`Normalize.css`修复，`Neat.css`融合重置与修复功能
- html{box-sizing: border-box;} _,_:before,X:after{box-sizing: inherit;} 通用配置

#### icon-font 与常用字体排版

- no-image 时代 不超过纯色为 2 的图像, [css icon](http://cssicon.space/#/)：纯 css 绘制 icon
- 宋体非宋体 黑体非黑体 Windows 下的宋体叫中易宋体`SimSun`，Mac 是华文宋体`STSong`。Windows 下的黑体叫中易黑体`SimHei`，Mac 是华文黑体`STHeiti`。
- 不要只写中文字体名，保证西文字体在中文字体前面。Mac->Linux->Windows
- 切忌不要直接使用设计师 PSD 的设计 font-family,关键时刻再去启动 font-face（`typo.css` 、 `Entry.css` 、`Type.css` ）
- `font-family: sans-serif;`系统默认，字体多个单词组成加引号。

#### css 绘制高级技巧

- border && border-radius 造就万千可能
- after && before 任何一个 HTML 元素都可以创造 3 个可以供我们操作的视觉元素，即三个矩形。
- box-shadow 是可以定义为任意颜色的，并且同一个元素可以投射出不同的 box-shadow。
  > `box-shadow: h-shadow v-shadow blur spread color inset;`: box-shadow 向框添加一个或多个阴影。该属性是由逗号分隔的阴影列表，每个阴影由 2-4 个长度值、可选的颜色值以及可选的 inset 关键词来规定。省略长度的值是 0。
  > `h-shadow`: 必需。水平阴影的位置。允许负值。\
  > `v-shadow`: 必需。垂直阴影的位置。允许负值。\
  > `blur`: 可选。模糊距离。\
  > `spread`: 可选。阴影的尺寸。\
  > `color`: 可选。阴影的颜色。\
  > `inset`: 可选。将外部阴影 (outset) 改为内部阴影。
- 渐变，`linear-gradient()`, `radial-gradient()`
  > `background: radial-gradient(shape size at position, start-color, ..., last-color);` \
  > `shape`: `ellipse` (默认): 指定椭圆形的径向渐变；`circle` ：指定圆形的径向渐变 \
  > `size`: 定义渐变的大小; `farthest-corner` (默认) : 指定径向渐变的半径长度为从圆心到离圆心最远的角; `closest-side` ：指定径向渐变的半径长度为从圆心到离圆心最近的边; `closest-corner` ： 指定径向渐变的半径长度为从圆心到离圆心最近的角; `farthest-side` ：指定径向渐变的半径长度为从圆心到离圆心最远的边 \
  > `position`: 定义渐变的位置。`center`（默认）：设置中间为径向渐变圆心的纵坐标值。`top`：设置顶部为径向渐变圆心的纵坐标值。`bottom`：设置底部为径向渐变圆心的纵坐标值。\
  > `start-color, ..., last-color`: 用于指定渐变的起止颜色。\
  >  \
  > `background: linear-gradient(direction, color-stop1, color-stop2, ...);`\
  > `direction`: 用角度值指定渐变的方向（或角度）。\
  > `color-stop1, color-stop2,...`:用于指定渐变的起止颜色。
- css 混合模式`mix-blend-mode`: 默认情况下是会混合所有比起层叠顺序低的元素, `background-blend-mode`: 背景的混合模式。可以是背景图片之间的混合，也可以是背景图片和背景色的混合，具体参数和 mix-blend-mode 一样
  > mix-blend-mode: normal; //正常 \
  > mix-blend-mode: multiply; //正片叠底 \
  > mix-blend-mode: screen; //滤色 \
  > mix-blend-mode: overlay; //叠加 \
  > mix-blend-mode: darken; //变暗 \
  > mix-blend-mode: lighten; //变亮 \
  > mix-blend-mode: color-dodge; //颜色减淡 \
  > mix-blend-mode: color-burn; //颜色加深 \
  > mix-blend-mode: hard-light; //强光 \
  > mix-blend-mode: soft-light; //柔光 \
  > mix-blend-mode: difference; //差值 \
  > mix-blend-mode: exclusion; //排除 \
  > mix-blend-mode: hue; //色相 \
  > mix-blend-mode: saturation; //饱和度 \
  > mix-blend-mode: color; //颜色 \
  > mix-blend-mode: luminosity; //亮度 \
  > mix-blend-mode: initial; //初始 \
  > mix-blend-mode: inherit; //继承 \
  > mix-blend-mode: unset; //复原

#### BFC IFC GFC FFC

##### BFC

> Box: CSS 布局的基本单位: Box 是 CSS 布局的对象和基本单位， 直观点来说，就是一个页面是由很多个 Box 组成的。元素的类型和 display 属性，决定了这个 Box 的类型。 不同类型的 Box， 会参与不同的 Formatting Context（一个决定如何渲染文档的容器），因此 Box 内的元素会以不同的方式渲染。\
> block-level box:display 属性为 block, list-item, table 的元素，会生成 block-level box。并且参与 block fomatting context；\
> inline-level box:display 属性为 inline, inline-block, inline-table 的元素，会生成 inline-level box。并且参与 inline formatting context；\
> Formatting context 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。最常见的 Formatting context 有 Block fomatting context (简称 BFC)和 Inline formatting context (简称 IFC)。

- 根元素
- `float`属性不为`none`
- `position`为`absolute`或`fixed`
- `display`为`inline-block`, `table-cell`, `table-caption`, `flex`, `inline-flex`
- `overflow`不为`visible`

#### 总结

- 其实以上的几个例子都体现了，BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
- IFC(Inline Formatting Contexts)直译为"内联格式化上下文"，IFC 的 line box（线框）高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的 padding/margin 影响)
- FFC(Flex Formatting Contexts)直译为"自适应格式化上下文"，display 值为 flex 或者 inline-flex 的元素将会生成自适应容器（flex container），
- GFC(GridLayout Formatting Contexts)直译为"网格布局格式化上下文"，当为一个元素设置 display 值为 grid 的时候，此元素将会获得一个独立的渲染区域，我们可以通过在网格容器（grid container）上定义网格定义行（grid definition rows）和网格定义列（grid definition columns）属性各在网格项目（grid item）上定义网格行（grid row）和网格列（grid columns）为每一个网格项目（grid item）定义位置和空间。
