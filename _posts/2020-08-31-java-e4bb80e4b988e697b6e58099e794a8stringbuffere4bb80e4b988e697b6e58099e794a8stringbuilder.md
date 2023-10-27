---
id: 244
title: 'Java-什么时候用StringBuffer什么时候用StringBuilder?'
date: '2020-08-31T16:02:35+08:00'
author: Aaron
layout: post
guid: 'http://47.101.191.3/?p=244'
permalink: /2020/08/31/java-%e4%bb%80%e4%b9%88%e6%97%b6%e5%80%99%e7%94%a8stringbuffer%e4%bb%80%e4%b9%88%e6%97%b6%e5%80%99%e7%94%a8stringbuilder/
views:
    - '128'
categories:
    - Programming
tags:
    - java语言特性
---

#### <div class="alert alert-info">1. [Java中的String，StringBuilder，StringBuffer三者的区别](https://www.cnblogs.com/su-feng/p/6659064.html)</div>

这三个类之间的区别主要是在两个方面，即运行速度和线程安全这两方面。

**运行速度：**

```
<pre class="prettyprint language-java">```java
<span class="token class-name">String</span> str<span class="token operator">=</span><span class="token string">"abc"</span><span class="token punctuation">;</span>
<span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>str<span class="token punctuation">)</span><span class="token punctuation">;</span>
str<span class="token operator">=</span>str<span class="token operator">+</span><span class="token string">"de"</span><span class="token punctuation">;</span>
<span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>str<span class="token punctuation">)</span><span class="token punctuation">;</span>
```
```

如果运行这段代码会发现先输出“abc”，然后又输出“abcde”，好像是str这个对象被更改了，其实，这只是一种假象罢了，JVM对于这几行代码是这样处理的，首先创建一个String对象str，并把“abc”赋值给str，然后在第三行中，其实JVM又创建了一个新的对象也名为str，然后再把原来的str的值和“de”加起来再赋值给新的str，而原来的str就会被JVM的垃圾回收机制（GC）给回收掉了，所以，str实际上并没有被更改，也就是前面说的String对象一旦创建之后就不可更改了。所以，Java中对String对象进行的操作实际上是一个不断创建新的对象并且将旧的对象回收的一个过程，所以执行速度很慢。

```
<pre class="prettyprint language-java">```java
<span class="token class-name">String</span> str<span class="token operator">=</span><span class="token string">"abc"</span><span class="token operator">+</span><span class="token string">"de"</span><span class="token punctuation">;</span>
<span class="token class-name">StringBuilder</span> stringBuilder<span class="token operator">=</span><span class="token keyword">new</span> <span class="token class-name">StringBuilder</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">append</span><span class="token punctuation">(</span><span class="token string">"abc"</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">append</span><span class="token punctuation">(</span><span class="token string">"de"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>str<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token class-name">System</span><span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>stringBuilder<span class="token punctuation">.</span><span class="token function">toString</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
```
```

这样输出结果也是“abcde”和“abcde”，但是String的速度却比StringBuilder的反应速度要快很多，这是因为第1行中的操作和  
String str=“abcde”;  
是完全一样的，所以会很快，而如果写成下面这种形式

```
<pre class="prettyprint language-java">```java
<span class="token class-name">String</span> str1<span class="token operator">=</span><span class="token string">"abc"</span><span class="token punctuation">;</span>
<span class="token class-name">String</span> str2<span class="token operator">=</span><span class="token string">"de"</span><span class="token punctuation">;</span>
<span class="token class-name">String</span> str<span class="token operator">=</span>str1<span class="token operator">+</span>str2<span class="token punctuation">;</span>
```
```

那么JVM就会像上面说的那样，不断的创建、回收对象来进行这个操作了。速度就会很慢。

**线程安全：**

在线程安全上，StringBuilder是线程不安全的，而StringBuffer是线程安全的

- 如果一个StringBuffer对象在字符串缓冲区被多个线程使用时，StringBuffer中很多方法可以带有synchronized关键字，所以可以保证线程是安全的，但StringBuilder的方法则没有该关键字，所以不能保证线程安全，有可能会出现一些错误的操作。所以如果要进行的操作是多线程的，那么就要使用StringBuffer，但是在单线程的情况下，还是建议使用速度比较快的StringBuilder。

我不知道为什么这个这么老的问题会出现在我的时间线上，看了一下回答，大多是2012，2013年的回答，照说那个年代，有些历史故事还很新鲜，却不知道为什么没有一个答案说到点子上。

stringbuffer固然是线程安全的，stringbuffer固然是比stringbuilder更慢，固然，在多线程的情况下，理论上是应该使用线程安全的stringbuffer的。

然而，然而，然而，有谁给我一个实际的案例来显示你需要一个线程安全的string拼接器？对不起，至少在我浅薄的十几年编程生涯中还没有遇到过，也许，仅仅是也许，这个地球上的确是存在这样的编程需求的，然而，它至少跟99.99…99%的程序员是无关的。**所以，他们的适用场景是什么?最简单的回答是，stringbuffer基本没有适用场景，你应该在所有的情况下选择使用stringbuiler**，除非你真的遇到了一个需要线程安全的场景，如果遇到了，请务必在这里留言通知我。

然后，补充一点，关于线程安全，即使你真的遇到了这样的场景，很不幸的是，恐怕你仍然有99.99…99%的情况下没有必要选择stringbuffer，因为stringbuffer的线程安全，仅仅是保证jvm不抛出异常顺利的往下执行而已，它可不保证逻辑正确和调用顺序正确。大多数时候，我们需要的不仅仅是线程安全，而是锁。

最后，为什么会有stringbuffer的存在，如果真的没有价值，为什么jdk会提供这个类？

答案太简单了，因为最早是没有stringbuilder的，sun的人不知处于何种愚蠢的考虑，决定让stringbuffer是线程安全的，然后大约10年之后，人们终于意识到这是一个多么愚蠢的决定，意识到在这10年之中这个愚蠢的决定为java运行速度慢这样的流言贡献了多大的力量，于是，在jdk1.5的时候，终于决定提供一个非线程安全的stringbuffer实现，并命名为stringbuilder。顺便，javac好像大概也是从这个版本开始，把所有用加号连接的string运算都隐式的改写成stringbuilder，也就是说，从jdk1.5开始，用加号拼接字符串已经没有任何性能损失了。

\-----------补充一个小小的修改----------如诸多评论所指出的，我上面说，"用加号拼接字符串已经没有任何性能损失了"并不严谨，严格的说，如果没有循环的情况下，单行用加号拼接字符串是没有性能损失的，java编译器会隐式的替换成stringbuilder，但在有循环的情况下，编译器没法做到足够智能的替换，仍然会有不必要的性能损耗，因此，用循环拼接字符串的时候，还是老老实实的用stringbuilder吧。

#### <div class="alert alert-success">2. 什么时候用StringBuffer什么时候用StringBuilder?</div>

- String：适用于少量的字符串操作的情况
- StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况
- StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况