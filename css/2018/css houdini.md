---
layout: page
title: css doodle
permalink: /css/2018_10_19_2
---

### css 魔术师

#### 样式中定义变量
```
<style>
    body {
        margin: 0;
        padding: 0;
        color: #ffffff;
        background: #0a0c2f;
    }

    body::after {
        content: '';
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        position: absolute;
        --star-opacity: .7;
        --star-density: .8;
        background: paint(sky);
    }
</style>
```

#### script 中读取
```
<script>
    if (!CSS in window || !CSS.paintWorklet) {
        alert('您的浏览器不支持CSS houdini')
    } else {
        CSS.paintWorklet.addModule('./sky.js');
    }
</script>
```

#### 定义 sky.js
```
class sky {
    constructor() {}
    static get inputProperties() {
        return ['--start-opacity', '--start-density']
    }

    paint(ctx, paintSize, properties) {
        console.log(arguments);

        let xMax = paintSize.width;
        let yMax = paintSize.height;

        let startOpacity = properties.get('--start-opacity');
        let startDensity = properties.get('--start-density') || 1;


    }
}
registerPaint('sky', sky);
```
