---
layout: page
title: ECMAScript5 核心技巧
permalink: /javascript/2018_8_13
---
### ECMAScript5 核心技巧

![原型链]({{ site.baseurl }}/{{ site.assets }}/prototype.png)

#### IIFE(立即调用函数表达式)是一个在定义时就会立即执行的 JavaScript 函数

> 这是一个`自执行匿名函数`的设计模式，主要包含两部分。\
> 第一部分是包围在`圆括号运算符()`里的一个匿名函数，这个匿名函数拥有独立的词法作用域，这不仅避免了外界访问此 IIFE 中的变量，而且又不会污染全局作用域。\
> 第二部分再一次使用（）创建了一个立即执行函数表达式，JavaScript 引擎到此将直接执行函数。

```
// 常规方式
(function(){
    alert('IIFE');
})()

// 转表达式方式，！+ - ~
!function(){
    alert('IIFE');
}
```

#### 全局作用域和函数级作用域

- 函数变量提升优先于变量，函数和变量同名且同时存在，这货没有值就会被直接忽略

```
(function(){
    alert(a);
    var a = 1;
    function a(){}
})(); // function a(){}

<!-- ==> 提升后 -->
(function(){
    function a(){}
    var a; // 函数和变量同名且同事存在，这货没有值就会被直接忽略
    alert(a);
    a = 1; // a的赋值保留当前的词法作用域
})();

(function(){
    var a = b = 1;

    <!-- 转换后 -->
    var a = 1;
    b = 1;
})();
alert(a); // 报错，not defined
alert(b); // 1
```

- es5 中只有函数级作用域，没有块级作用域

```
<!-- 没有函数，则提升到全局 -->
if (false){
    var a = 1;
}
alert(a); // undefined

<!-- 提升后 -->
var a;
if (false) {
    a = 1;
}
alert(a); // undefined

<!-- 有函数，则提升到函数顶端 -->
function test() {
    if (false) {
        var a = 1;
    }
    alert('inner ' + a); // undefined
}
test(); // inner undefined
alert(a); // a is not defined(报错)

<!-- 转换后 -->
function test() {
    var a;
    if (false) {
        a = 1;
    }
    alert('inner ' + a);
}
test();
alert(a);
```

#### 块级作用域

- function block(){}
- if(){}, 这个时候需要 es6 中 `let`, `const` 配合

```
if (false) {
    let a = 1;
}
alert(a); // 报错，not defined
```

- try{}catch(e){}

```
if (true) {
    try {
        throw 111;
    } catch(a) {
        alert(a); // 111
    }
}
alert(a); // 报错，not defined
```

- with 只对对象中存在的属性有用，但是对象中不存在的属性，with 会生成全局变量

```
<!-- with 只对对象中存在的属性有用, 不存在，则生成全局变量-->
var obj = {
    a: 1
};
with(obj) {
    b = 2;
};
alert(obj.b); // undefined
alert(b); // 2
```

#### 变量回收

```
function test(){
    var a = 1;
}
test(); // 用完之后 a 会被回收

function test(){
    var a = 1;
    return function(){
        a++; // 闭包占用后就不会被回收
        eval(""); // 这种情况也不会被回收，因为 eval 不确定会不会调用 a
        window.eval(""); // 作用域改变，这中情况会被回收
        with(a){} // 这种情况也不会被回收
        try{}catch(){} // 也不会
    }
}
test(); // 用完之后 a 会被回收
```

#### VO、AO

- 变量对象（缩写为 VO）：就是与执行上下文相关的对象，它储存以下内容：
  > 变量（var，VariableDeclaration）\
  > 函数声明（FunctionDeclaration, 缩写为 FD）\
  > 函数的形参
- Arguments Objects 是函数上下文里的激活对象，AO 中的内部对象包括下列属性：
  > callee: 指向当前函数的引用；\
  > length: 真正传递的参数的个数；\
  > properties-indexes(字符串类型的整数）属性的值就是函数的参数值（按照参数列表从左到右排列）。properties-indexes 内部元素的个数等于 arguments.length. properties-indexes 的值和实际传递进来的参数之间是共享的。(共享与不共享的区别可以对比理解为引用传递与值传递的区别)
- 原理：执行上下文的代码被分成两个基本的阶段来处理；进入执行上下文，执行代码：
  > 当进入执行上下文（代码执行之前时）时，VO 已经被下列属性填充满：1、函数的所有形式参数（如果我们是在函数执行上下文中）；2、所有函数声明（FD）;3、所有变量声明（var）。\
  > 函数表达式（FunctionExpression，FE）而不是函数声明不会影响 VO

#### this(谁调用，this 就取谁)

- 谁调用 this 就指向谁

```
this.a = 20;
var obj = {
    a: 30,
    init: function(){
        alert(this.a);
    }
};
obj.init(); // 30

<!-- 谁调用取谁 -->
var obj2 = obj.init;
obj2(); // 20
```

- this 找不到对应执行体的时候，会指向 window

```
this.a = 22;
var obj3 = {
    a: 30,
    init: function(){
        function test(){
            // 找不到对应执行体的时候，this会指向window
            alert(this.a);
        }
        test();
    }
};
var obj4 = obj3.init;
obj4(); // 22
obj3.init(); // 22
```

- => 箭头函数, bind 父级 this

```
this.a = 20;
var obj = {
    a: 30,
    init:()=>{
        alert(this.a);
    }
};
obj.init(); // 20
```

- this 优先于原型链 prototype 查找

```
function test(){
    this.a = 20;
}
test.prototype.a = 30;
alert((new test()).a); // 20
```

#### class 语法糖，实现原理是基于原型链

```
class test {
    // constructor = test.prototype.constructor = test;
    constructor(){
        this.qq = 2016;
    }
    a(){
        alert(1)
    }
}
test.prototype.a = function(){
    alert(2);
}
new test().a() // 2

<!-- class 编译后 -->
function test(){
    this.qq = 2016;
}
test.prototype.a = function(){
    alert(1);
}
```

#### let 暂时性死区、块级作用域

```
if(true){
    i = 5;
    let i; // es6 规定暂时性死区，块级作用域下，必须先声明再使用
}
alert(i); // 报错，i is not defined
```

#### js 单线程是因为需要操作 dom

#### 按值传递，按引用传递，函数的参数是按值传递，但是传递的对象是引用传递

- 按值传递（简单基本类型， number,boolean,string）

- 按引用传递（array, object）

```
// 参数 m 是按照值传递，m指向的对象是按引用传递，这里的m只是一个形参名称，可以随意变换
function test(m){
    // 重写
    // 指针指向改变，外部拿不到
    m = {
        v: 5
    }
}
var m = {
    k: 30
};
alert(m.v); // undefined
```
