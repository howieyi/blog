---
layout: page
title: CSS3 与数学的巧妙应用
permalink: /css/2018_8_12
---

### css3 与数学巧妙应用

#### [`clip-path`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/clip-path) 属性可以创建一个只有元素的部分区域可以显示的剪切区域。区域内的部分显示，区域外的隐藏。剪切区域是被引用内嵌的 URL 定义的路径或者外部 svg 的路径，或者作为一个形状例如 circle().。clip-path 属性代替了现在已经弃用的剪切 clip 属性。

- `<clip-source>`: 用`<url>`表示剪切元素的路径
- `inset()`, `circle()`, `ellipse()`, `polygon()`: 一个`<basic-shape>` 方法. 这种形状将会利用指定的`<geometry-box>`来定位和固定基本形状。如果没有 geometry box（几何盒模型）特别指出的话，border-box 将会是默认的盒模型。
- `<geometry-box>`: 如果同`<basic-shape>`一起声明，它将为基本形状提供相应的参考盒子。通过自定义，它将利用确定的盒子边缘包括任何形状边角（比如说，被 border-radius 定义的剪切路径）。几何体盒子将会有以下的值：
  > `fill-box`: 利用对象边界框作为引用框。\
  > `stroke-box`: 使用笔触边界框作为引用框 \
  > `view-box`: 使用最近的 SVG 视口作为引用框。如果 viewBox 属性被指定来为元素创建 SVG 视口，引用框将会被定位在坐标系的原点，引用框位于由 view-box 属性建立的坐标系的原点，引用框的尺寸用来设置 viewbox 属性的宽高值。\
  > `margin-box`: 使用 margin box 作为引用框 \
  > `border-box`: 使用 border box 作为引用框. \
  > `padding-box`: 使用 padding box 作为引用框. \
  > `content-box`: 使用 content box 作为引用框
- `none`: 这里没有创建的剪切路径。

```
clip-path: circle(40%);
clip-path: ellipse(130px 140px at 10% 20%);
clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);

/* Keyword values */
clip-path: none;

/* Image values */
clip-path: url(resources.svg#c1);

/* Box values
clip-path: fill-box;
clip-path: stroke-box;
clip-path: view-box;
clip-path: margin-box
clip-path: border-box
clip-path: padding-box
clip-path: content-box

/* Geometry values */
clip-path: inset(100px 50px);
clip-path: circle(50px at 0 100px);
clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);

/* Box and geometry values combined */
clip-path: padding-box circle(50px at 0 100px);

/* Global values */
clip-path: inherit;
clip-path: initial;
clip-path: unset;
```

#### [`cubic-bezier`](http://cubic-bezier.com/#.17,.67,.83,.67) 贝塞尔曲线，描述动画路径

- 常用的 linear, ease, ease-in, ease-out, ease-in-out 都是基于贝塞尔曲线
    ![贝塞尔曲线]({{ site.baseurl }}/{{ site.assets }}/bezier.png)

#### `matrix`矩阵：描述位移，像我们往常使用的 rotate,scale,skew...等位移变化都是基于`matrix`矩阵实现

- [生成工具](https://meyerweb.com/eric/tools/matrix/)
