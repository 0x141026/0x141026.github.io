---
id: 242
title: 动态类型，静态类型；强类型，弱类型语言
date: '2020-01-02T17:52:08+08:00'
author: Aaron
layout: post
guid: 'http://47.101.191.3/?p=242'
permalink: /2020/01/02/%e5%b8%b8%e8%a7%81%e5%8a%a8%e6%80%81%e7%b1%bb%e5%9e%8b%ef%bc%8c%e9%9d%99%e6%80%81%e7%b1%bb%e5%9e%8b%ef%bc%9b%e5%bc%ba%e7%b1%bb%e5%9e%8b%ef%bc%8c%e5%bc%b1%e7%b1%bb%e5%9e%8b%e8%af%ad%e8%a8%80%e5%88%86/
seo_description_value:
    - 常见动态类型，静态类型；强类型，弱类型语言分布图
seo_keywords_value:
    - 编程语言特性
views:
    - '92'
categories:
    - Programming
tags:
    - 编程语言特性
---

![](https://z3.ax1x.com/2021/03/21/65zG7V.jpg)

一、编译时就知道变量类型的是静态类型；运行时才知道一个变量类型的叫做动态类型

二、不允许隐式转换的是强类型，允许隐式转换的是弱类型

- trapped errors：导致程序终止执行（程序意识到出错，使用对应的错误处理机制），如除 0，Java 中数组越界访问
- untrapped errors：程序出错后继续执行（其实并不一定保证继续执行，程序本身并不知道出错，也没有对应的错误处理机制），如 C 语言里的缓冲区溢出，Jmp 到错误地址

**举个栗子：**

在 Python 中执行 `test = '666' / 3` 你会在运行时得到一个 TypeError 错误，相当于运行时排除了 untrapped error，因此 Python 是动态类型，强类型语言。

在 JavaScript 中执行 `var test = '666' / 3'` 你会发现 test 的值变成了 222，因为这里发生了隐式转换，因此 JavaScript 是动态类型，弱类型的。更为夸张的是 `[] == ![]` 这样的代码在 JavaScript 中返回的是 true，这里是具体的 原因。

在 Java 中执行 `int[] arr = new int[10]; arr[0] = '666' / 3;` 你会在编译时期得到一个语法错误，这说明 Java 是静态类型的，执行 `int[] arr = new int[10]; arr[11] = 3;` 你会在运行时得到数组越界的错误（trapped error），这说明 Java 通过自身的类型系统排除了 untrapped error，因此 Java 是强类型的。

而 C 与 Java 类似，也是静态类型的，但是对于 `int test[] = { 1, 2, 3 }; test[4] = 5;` 这样的代码 C 语言是没办法发现你的问题的，因此这是 untrapped error，因此我们说 C 是弱类型的。

**P.S:**

另外，由于强类型语言一般需要在运行时运行一套类型检查系统，因此强类型语言的速度一般比弱类型要慢，动态类型也比静态类型慢，因此在上述所说的四种语言中执行的速度应该是 C &gt; Java &gt; JavaScript &gt; Python。但是强类型，静态类型的语言写起来往往是最安全的。