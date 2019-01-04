---
layout: page
title: css doodle
permalink: /css/2018_10_19
---

### [< css-doodle /> 用于使用CSS绘制图案的Web组件](https://css-doodle.com/)

#### 安装
```
$ npm install css-doodle
```

#### html 引入 js
```
<script src="../node_modules/css-doodle/css-doodle.min.js"></script>
```

#### 绘制图形
```
<css-doodle>
    :doodle {
    @grid: 10 / 10vmax;
    background: #0a0c27;
    }
    --hue: calc(180 + 1.5 * @row() * @col());
    background: hsl(var(--hue), 50%, 70%);
    margin: -.5px;
    transition: @r(.5s) ease;
    clip-path: polygon(@pick(
    '0 0, 100% 0, 100% 100%',
    '0 0, 100% 0, 0 100%',
    '0 0, 100% 100%, 0 100%',
    '100% 0, 100% 100%, 0 100%'
    ));
</css-doodle>
```

#### 使用动画
```
<css-doodle>
    :doodle {
    @grid: 1x10 / 61.8vmin;
    }
    @size: calc(@index() * 10%);
    @place-cell: center;
    border-radius: 50%;
    border-style: dashed;
    border-width: calc(@index() * 1vmin);
    border-color: hsla(calc(20 * @index()), 70%, 60%, calc(3 / @index() * .8));
    --delay: @rand(10s, 20s);
    --rotateLeft: @rand(360deg);
    --rotateRight: @rand(var(--rotateLeft) + @pick(1turn, -1turn));
    animation: spin var(--delay) linear infinite;
    @keyframes spin {
    from{ transform: rotate(var(--rotateLeft)) }
    to{ transform: rotate(var(--rotateRight)) }
    }
</css-doodle>
```