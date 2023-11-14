---
id: 241
title: 'html页面调用js文件里的函数报错onclick is not defined处理方法'
date: '2020-01-09T09:23:35+08:00'
author: Aaron
layout: post
guid: 'http://185.199.109.153/?p=241'
permalink: /2020/01/09/html%e9%a1%b5%e9%9d%a2%e8%b0%83%e7%94%a8js%e6%96%87%e4%bb%b6%e9%87%8c%e7%9a%84%e5%87%bd%e6%95%b0%e6%8a%a5%e9%94%99onclick-is-not-defined%e5%a4%84%e7%90%86%e6%96%b9%e6%b3%95/
seo_description_value:
    - js
seo_keywords_value:
    - js
views:
    - '79'
categories:
    - Programming
tags:
    - js
---

今天处理html标签里的onclick功能的时候总是报错：Uncaught ReferenceError: dosave is not defined(…)

找了半天都没发现错在哪，最后发现原来是我写法不对，正确写法如下：

html：

&lt;input type="button" value="立即登录" οnclick="dosave();"/&gt;  
js：

dosave = function (){  
alert("成功啦！");  
}  
***错误写法一般有以下两种，很致命：***

function dosave(){  
alert("会报错！！");  
}  
和

var dosave = function (){  
alert("会报错！！");  
}  
为什么会这样，因为：

html页面调用js文件里的函数，写法必须为dosave = function (){}形式，其他方式写，html页面会搜索不到该函数。

\------------------------------------------------------------------分割线--------------------------------------------------------------------------------------

1.这个问题很奇特。很多人平常使用var dosave = function(){}和function dosave(){}都没问题，但是突然一天出现用不了的情况了，我当时就是这样的情况；还有的同学在HBuidlder运行没问题，换eclipse就不起作用。

2.这三种定义函数的写法都是正确的，只不过作用域不同。

3.我们知道var dosave = function(){}和function dosave(){}是等价的，是最常用的定义函数方式，区别在于function dosave(){}可以进行声明提升，而var dosave = function(){}必须先定义才能使用。

4.dosave = function(){}的写法会把dosave函数作为全局作用域函数，相当于windows对象作为他的作用域，所以可以被调用到。

5.有同学给出了一种解决办法，不过我当时就没用$(function(){ })，所以对我的情况不管用：

1）定义的方法 用funcation 方法名（）{} ，这样写没有问题，不过js中千万别把方法写在jQuery的入口函数$(function(){ })中，这样相当于方法中方法，所以查找不到。

2）将方法放在 $().ready(function () {});之外后，就可以正常执行了。

6.当大家遇到莫名报错时这三种定义函数的写法都试试吧，说不定能帮助到大家，算是提供一种思路。