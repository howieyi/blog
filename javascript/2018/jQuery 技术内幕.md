---
layout: page
title: jQuery 技术内幕
permalink: /javascript/2018_8_17
---

### jQuery 技术内幕

#### jQuery 构造函数

```
// 这里的参数 undefined 拿到的是真的 undefined
var jQuery = (function(window, undefined){
    var jQuery = function(selector) {
        return new jQuery.fn.init(selector);
    };
    jQuery.fn = jQuery.prototype = {
        init: function(){ },
        extend: function(){ }
    };
    // 可以共用 jQuery 的 this
    // ==> jQuery.fn.init = jQuery
    jQuery.fn.init.prototype = jQuery.fn;

    // 返回 jQuery
    return jQuery;
})(window);

jQuery.fn.extend // 对 jQuery 的原型链进行扩展
jQuery.extend // 直接添加 jQuery 静态
```

#### 重载

```
function addMethod(obj, name, fn){
    var old = obj[name];
    obj[name] = function(){
        // arguments 实参
        if(fn.length === arguments.length){
            return fn.apply(this, arguments);
        }else if{
            return old.apply(this, arguments);
        }
    }
}
var objs = [1, 2, 3];
addMethod(objs, 'find', function(){return 0;});
addMethod(objs, 'find', function(one){return 1;});
addMethod(objs, 'find', function(one, two){return 2;});
```

#### 链式调用

```
var obj = {
    a: function(){
        return this;
    },
    b: function(){
        return this;
    }
};

obj.a().b(); // 链式调用，每个 function 返回this
```

#### >>> 0 按位操作（二进制操作，加快运算）

```
var obj = new Array(10);
var length = obj.length >>> 0; // 二进制位运算，加快运算
```

#### 短路操作 && ||

```
// 避免使用 if else 逻辑
a && a();
b || a();
```

#### sizzle jQuery 选择器引擎

#### hook 映射 表驱动原理（用来解决一种或多种情况的处理）

```
(function(window, undefined){
    var class2Types = {};
    jQuery.each('Array Object Number Function Error Boolean Date RegExp Symbol String').split(' '), function(type){
        class2Types['[object ' + type + ']'] = name;
    });
})(window);

// 使用
```

#### 连贯接口

- 链式调用
- 命令查询媒体（重载）
- 参数映射

#### ready(DOMContentedloaded)

```
// ==> $.ready();
window.addEventListener('DOMContentedloaded', function(){
    // ready....
});

// ie 利用滚动条的一个方法，抛错处理
(function(){
    function IEContentLoaded(){
        (function(){
            try {
                document.documentElement.doScroll('left');
            } catch(e) {
                setTimeout(arguments.callee, 50);
            }
        })();
    }
})();
```
