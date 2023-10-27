---
id: 258
title: 'javascript中的立即执行函数(function(){})()'
date: '2020-05-20T20:58:24+08:00'
author: Aaron
layout: post
guid: 'http://47.101.191.3/?p=258'
permalink: /2020/05/20/javascript%e4%b8%ad%e7%9a%84%e7%ab%8b%e5%8d%b3%e6%89%a7%e8%a1%8c%e5%87%bd%e6%95%b0function/
views:
    - '134'
seo_description_value:
    - 立即执行函数
seo_keywords_value:
    - js;立即执行函数
categories:
    - Programming
tags:
    - 立即执行函数
---

# 一、立即执行函数的基本介绍

**P.S. 立即执行函数最好放在页面文档全部加载后，比如放在$(function(){})中。**

要理解立即执行函数(function(){})()，先了解些函数的基本概念（函数声明、函数表达式、匿名函数）。

**函数声明**：使用function声明函数，并指定函数名。

<div class="cnblogs_code">```
function setFn() {
    // coding   
}
```

</div>**函数表达式**：使用function声明函数，但未指定函数名，将匿名函数赋予一个变量。

<div class="cnblogs_code">```
var setFn = function() {
    // coding
}
```

</div>**匿名函数**：使用function关键字声明函数，但未指定函数名。匿名函数属于函数表达式，匿名函数有很多作用，赋予一个变量则创建函数，赋予一个事件则成为事件处理程序或创建闭包等等。

<div class="cnblogs_code">```
function() {
    // coding
}
```

</div>函数声明与函数表达式的不同在于：

1\. 函数声明可在当前作用域下提前调用执行，函数表达式需等执行到该函数后，方可执行，不可提前调用。

<div class="cnblogs_code">```
setFn()
function setFn() {
    // coding  
}
// 正常，函数声明可提前调用

setFn()
var setFn = function() {
    // coding
} 
// 报错，setFn未保存对函数的引用，函数调用需放在函数表达式后面
```

</div>2\. 函数表达式可直接在函数后加括号调用。

<div class="cnblogs_code">```
var setFn = function() {
    console.log(2)
}()

// 2   解析至此，可直接执行调用
```

</div>立即执行函数(function(){})()可以看出很像函数表达式的调用，但为什么要加括号呢？如果不加括号：

<div class="cnblogs_code">```
function(){
    console.log(1)
}()

// 报错，函数需要函数名

解析： 虽然匿名函数属于函数表达式，但未进行赋值，所以javascript解析时将开头的function当做函数声明，故报错提示需要函数名
```

</div>立即执行函数里面的函数必须是函数表达式，所以由var setFn = function() {*}()*可以理解为在匿名函数前加了 = 运算符后，将函数声明转化为函数表达式，所以拿！，+，-，（）...等运算符来测试下是否如此。

<div class="cnblogs_code">```
!function(){
    console.log(1)
}()
// 1
    
+function(){
    console.log(2)
}()
// 2
    
-function(){
    console.log(3)
}()
// 3
    
(function(){
    console.log(4)
})()
// 4
```

</div>由此可见，加运算符确实可将函数声明转化为函数表达式，而之所以使用括号，是因为括号相对其他运算符会更安全，可以减少不必要的麻烦。

立即执行函数与正常函数传参形式是一致的。

<div class="cnblogs_code">```
(function(a, b){
    console.log(a + b);
})(1, 2)
// 3
```

</div>(function(){}())这样写的好处是在内部定义的变量不会跟外部的变量有冲突，达到保护内部变量的作用。

- - - - - -

# **二、立即执行函数使用时机及好处**

（一）基本结构

这样的函数有多常用呢，我们可以看看下面的代码：

<div class="cnblogs_code">```
(function( window, undefined ) {
//……
})(window);
```

</div>这段代码，大家一定不会陌生。是的，它就是我们"Write less, do more"的jQuery。

jQuery整个文件就是一个立即执行函数。

(function(){})(); 是立即执行函数常用的表现形式之一。

另一种也很常用：

(function(){}());

以上两种是比较常用的写法，但立即执行函数的写法因人而异。记住以下两点就可以了。

如果是函数表达式，可直接在其后加"()"立即执行。

如果是函数声明，可以通过"()"、"+"、"-"、"void"、"new"等运算符将其转换为函数表达式，然后再加"()"立即执行。

比如，下面的写法也是没有问题的。

<div class="cnblogs_code">```
void function(){}(alert("ok"));
```

</div>在执行前，可以在最后调用的"()"传入我们需要的参数，比如jQuery就把window对象作为实参传入了立即函数内部。

（二）使用时机

什么时候需要用到立即执行函数呢？

1.当我们需要写一个js文件，并且复用率很高的时候，建议使用。

2.如果声明的函数只需要调用一次，建议使用。

3.独立模块，这个和第一点差不多。单独提出来，是想强调一下立即执行函数的好处，开发时，它能做到各模块的低耦合，减少对全局作用域的污染。

（三）实例及好处

无实例，无真相。找什么实例好呢？还是我们的<span class="cnblogs_code_collapse">jQuery 1.4.4</span>吧。

这个立即执行函数是比较庞大，所以我选取的是1.4.4这样一个比较老的版本，但也足以用来进行说明。

1.整个jQuery占用全局作用域两个变量，一个是jQuery，另一个是$。而且占用两个还是为了方便我们书写。其实两个变量是完全相同的，在第908行，我们可以看到。

<div class="cnblogs_code">```
// Expose jQuery to the global object
return (window.jQuery = window.$ = jQuery);
```

</div>jQuery内部封装的变量，我们可以直接通过$来访问。这样，避免了声明不必要的全局变量。

这里的jQuery可谓起到了一个命名空间的作用。

试想，如果我们引用了另一个js插件superQuery，它占用了一个全局变量，声明window.superQuery=superQuery;

那即便superQuery内部声明了和jQuery同名变量，它们命名空间不同，实际上，并不会造成冲突。

2.我们再来看913-1105行。

<div class="cnblogs_code">```
(function(){
jQuery.support = {};
//……
})();
```

</div>内部主要为创建了jQuery.support。这个创建工作只需要执行一次，所以也使用了立即执行函数。

而巧妙的是，再通过为support添加一系列的内容，就轻松将其暴露在我们可访问的范围之类了。同时，并未造成全局作用域污染。

3.参数和返回值

既然是函数，不可避免地要提一下参数和返回值。

立即函数内部是可以访问外部变量的，所以很多情况下，我们并不需要传参数。如：jQuery的window实参，如果不传入。内部也是可以直接使用的。

返回值也可以直接返回给立即执行函数外的某个变量的一个对象属性（注意，外部变量var a=1;是不能通过a.newAttribute=inParameter来赋值的。）

然而，从代码的可读性等方面考虑，我们显式地传入需要的参数是一个好习惯。

（四）注意点

立即执行函数通常作为一个单独模块使用。一般没有问题，但是，建议在自己写的立即执行函数前加分号，这样可以有效地与前面代码进行隔离。否则，可能出现意想不到的错误。

如：

<div class="cnblogs_code">```
        var c = 12
        var d = c
        (function () { var e = 14; }())
```

</div>会报这样一个错误：

![](https://s4.ax1x.com/2021/12/22/TlTQcF.png)

因为在我们立即执行函数模块前面代码没有一个分号来断句。那编译器就把前面的c和后面的语句当作函数调用来看了。

所以，由于很多时候，在立即执行函数之前的代码我们无法控制，为了良好的容错能力。我们一般在立即执行函数前加个分号与前面的代码断开，避免解析错误。