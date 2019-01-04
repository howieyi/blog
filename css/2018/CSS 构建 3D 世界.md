---
layout: page
title: CSS 构建 3D 世界
permalink: /css/2018_8_8
---

### CSS 构建 3D 世界

css 3d、陀螺仪、球面等

#### css 3d 绘制立方体

- [transform-style](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-style) 设置元素的子元素是否位于 3d 空间（该属性不被自动继承）

  > 1. `preserve-3d`: 指定子元素定位在 3d 空间
  > 2. `flat`: 指定元素位于此元素所在平面内

- [transform-function](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-function) css 数据类型用于对元素的显示做变换，通常，这种变换可以由矩阵表示，并且可以使用每个点上的矩阵乘法来确定所得到的图像。

  > 1. `matrix(a, b, c, d, tx, ty)`: 用六个指定的值来指定一个均匀的二维（2D）变换矩阵。a, b, c, d 以 number 格式来描述线性变换； tx, ty 以 number 格式来描述变换的量
  > 2. `matrix3d(a1, b1, c1, d1, a2, b2, c2, d2, a3, b3, c3, d3, a4, b4, c4, d4)`: 用一个 4\*4 的齐次矩阵来描述一个三维（3D）变换。a1 b1 c1 d1 a2 b2 c2 d2 a3 b3 c3 d3 d4 以 number 格式来描述线性变换；a4 b4 c4 以 number 格式来描述变换的量
  > 3. `perspective(l)` : 定义了 z=0 平面与用户之间的距离，以便给三维定位元素一定的透视度。当每个 3D 元素的 z>0 时会显得比较大，而在 z<0 时会显得比较小。其影响的程度由这个属性的值来决定。
  > 4. `rotate(a)`: 定义一个旋转属性，将元素在不变形的情况下旋转到不动点周围；a 代表旋转的角度，单位 deg，正负来决定顺时针或逆时针；
  > 5. `rotate3d(x, y, z, a)`: 定义了一个 3D 的旋转功能，该旋转使元素能绕固定轴移动而不变形。x, y, z 对应旋转向量的 x 坐标，y 坐标，z 坐标；a 代表旋转的角度， 正负来决定顺时针或逆时针；
  > 6. `rotateX(a)`: 将元素在横坐标上旋转而不使其变形的方法。rotate3D(1, 0, 0, a)的简写形式。
  > 7. `rotateY(a)`: 将元素在纵坐标上旋转而不使其变形的方法。rotate3D(0, 1, 0, a)的简写形式。
  > 8. `rotateZ(a)`: 将元素在 z 轴 上旋转而不使其变形的方法。rotate3D(0, 0, 1, a)的简写形式。
  > 9. `scale(sx[, sy])`: 改变元素的大小，可以增大或减小元素的大小，缩放量由矢量定义，并且可以使在一个方向上比另一个方向更多。sx（number）代表缩放矢量的横坐标；sy（number）代表缩放矢量的纵坐标，如果不存在，则起默认值为 sx，使元素均匀缩放。
  > 10. `scale3d(sx, sy, sz)`: 改变元素的大小，缩放量由矢量定义，因此可以改变不同方向的尺寸。sx, sy, sz 分别代表缩放矢量的横、纵、z 轴坐标。
  > 11. `scaleX(sx)`: scale3d(sx, 1, 1);
  > 12. `scaleY(sy)`: scale3d(1, sy, 1);
  > 13. `scaleZ(sz)`: scale3d(1, 1, sz);
  > 14. `skew(ax[, ay])`: 是一种用于拉伸，或者说是平移，该函数会使得每个方向上扭曲元素上的每个点以一定角度。这是通过将每个坐标增加一个与指定角度成比例的值和到原点的距离来完成的。离原点越远，拉伸的值就越大。ax, ay 角度，表示用于沿着横、纵坐标扭曲元素的角度。
  > 15. `skewX(ax)`: 水平拉伸
  > 16. `skewY(ay)`: 垂直拉伸
  > 17. `translate(tx[, ty])`: 用于移动元素在平面上的位置
  > 18. `translate3d(tx, ty, tz)`: 用于移动元素在 3d 空间中的位置；tz 不能使用百分比（会成为无效属性）

- [transform-origin](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-origin) 更改一个元素变形的原点。
  > transform-origin: center;
  > transform-origin: top left;
  > transform-origin: 50px 50px;
  > transform-origin: bottom right 60px;

#### 陀螺仪

> 陀螺仪又叫角速度传感器，是不同于加速度计（G-sensor）的，他的测量物理量是偏转、倾斜时的转动角速度。在手机上，仅用加速度计没办法测量或重构出完整的 3D 动作，测不到转动的动作的，G-sensor 只能检测轴向的线性动作。但陀螺仪则可以对转动、偏转的动作做很好的测量，这样就可以精确分析判断出使用者的实际动作。而后根据动作，可以对手机做相应的操作！

- `deviceorientation`: 设备的物理方向信息，表示为一系列本地坐标系的旋角。设备在方向发生改变是触发

  > `event.absolute`: 表示该设备是否提供绝对定位数据 (这个数据是关于地球的坐标系) 或者使用了由设备决定的专门的坐标系.
  > `event.alpha`: 返回设备旋转时 Z 轴的值；即：设备围绕屏幕中心扭转的角度。 \
  > `event.beta`: 返回设备旋转时 X 轴的值；即: 角度的数值，范围介于`-180 ~ 180`，表示设备正在向前或向后倾斜。\
  > `event.gamma`: 返回设备旋转时 Y 轴的值;即，多少度，介于之间`-90 ~ 90`，通过该装置被接通向左或向右。

- `devicemotion`: 提供设备的加速信息。设备在加速度发生改变是触发

  > `event.acceleration`: 返回设备的加速度记录（单位：m / s2）。如果硬件无法从 `acceleration` 数据中移除重力加速度，则该值在 `event` 中可能并不存在，你应当使用 `event.accelerationIncludingGravity` 代替
  > `event.accelerationIncludingGravity`: 返回设备的加速度的记录（单位：m / s2），此值是由用户引起的设备的加速度和由重力加速度的总和。x: 表示 x 轴（西到东）上的加速度, y: 表示 y 轴（南到北）上的加速度, z: 表示 z 轴（下到上）上的加速度 \
  > `event.rotationRate`: 设备围绕其每个轴（x、y、z）旋转的速率（单位：度/秒）。`alpha`: 设备沿着垂直屏幕的轴的旋转速率 (桌面设备相对于键盘)，`beta`: 设备沿着屏幕左至右方向的轴的旋转速率(桌面设备相对于键盘)，`gamma`: 设备沿着屏幕下至上方向的轴的旋转速率(桌面设备相对于键盘)\
  > `event.interval`: 从设备获取数据的频率，单位是毫秒

- `compassneedscalibration`: 用于通知 web 站点使用罗盘信息校准上述事件

```
var position = {
    alpha: 0,
    beta: 0,
    gamma: 0
}, last = {
    x: 0,
    y: 0,
    z: 0
}, speed = 30;

function moveBox() {
    var box = document.querySelector('.cube');
    box.style.transform = 'rotateX(' + position.alpha + 'deg) rotateY(' + position.beta +
        'deg) rotateZ(' + position.gamma + 'deg) translateZ(80px)';
}

window.addEventListener('deviceorientation', function (event) {
    // position.alpha = event.alpha; // z轴为轴 0 ~ 360
    // position.beta = event.beta; // x轴为轴 -180 ~ 180
    // position.gamma = event.gamma; // y轴为轴 -90 ~ 90
    moveBox();
});

window.addEventListener('devicemotion', function (event) {
    // 设备绕 x,y,z 轴旋转的角度
    Object.assign(position, event.rotationRate);

    // log(['devicemotion:->', 'acceleration@', JSON.stringify(event.acceleration),
    //     'accelerationInc@', JSON.stringif(event.accelerationIncludingGravity),
    //     'rotationRate@', JSON.stringify(event.rotationRate),
    //     'absolute@', event.absolute
    // ].join('__'));

    // 摇一摇
    var aig = event.accelerationIncludingGravity;
    if (Math.abs(aig.x - last.x) > speed || Math.abs(aig.y - last.y) > speed || Math.abs(aig.z -
            last.z) > speed) {
        alert('摇一摇');
    }
});

window.addEventListener('compassneedscalibration', function (event) {
    alert('罗盘需要校准');
    event.preventDefault();
});
```

#### 淘宝造物节活动要点

- 绘制全景：根据半径`radius`和图片张数`count`，`transform: rotateY(360/count * 图片index) translateZ(radius)`
- 计算全景半径：radius = 图片宽度 / 2 / Math.tan(360 / 图片张数 _ Math.PI _ 180);
  ![计算公式]({{ site.baseurl }}/{{ site.assets }}/radius.jpg)
- 计算 `touch` 移动角度：degY = -Math.atan2(x 轴滑动坐标差, radius) / Math.PI \* 180
