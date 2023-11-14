---
id: 248
title: 在centos后台运行python程序（nohup命令）
date: '2021-03-21T23:52:55+08:00'
author: Aaron
layout: post
guid: 'http://185.199.109.153/?p=248'
permalink: /2021/03/21/%e5%9c%a8centos%e5%90%8e%e5%8f%b0%e8%bf%90%e8%a1%8cpython%e7%a8%8b%e5%ba%8f%ef%bc%88nohup%e5%91%bd%e4%bb%a4%ef%bc%89/
views:
    - '266'
seo_description_value:
    - 在centos后台运行python程序（nohup命令）
seo_keywords_value:
    - nohup
categories:
    - Programming
tags:
    - centos
    - nohup命令
---

在服务器上，为了退出终端，程序依然能够运行，需要设置程序在后台运行。

关键的命令：`nohup`

## <a name="t0"></a><a name="t0"></a>\*基本用法：

进入要运行的py文件目录前

nohup python -u test.py &gt; test.log 2&gt;&amp;1 &amp;

## <a name="t2"></a><a name="t2"></a>\*含义解释：

nohup 不挂起的意思

python test.py python运行test.py文件

-u 代表程序不启用缓存，也就是把输出直接放到log中，没这个参数的话，log文件的生成会有延迟

&gt; test.log 将输出日志保存到这个log中

2&gt;1 2与&gt;结合代表错误重定向，而1则代表错误重定向到一个文件1，而不代表标准输出

2&gt;&amp;1 换成2&gt;&amp;1，&amp;与1结合就代表标准输出了，就变成错误重定向到标准输出

&amp; 最后一个&amp; ，代表该命令在后台执行

## <a name="t4"></a><a name="t4"></a>\*命令运行后会有提示，示例：

\[1\] 2880

代表进程2880中运行。

## <a name="t5"></a><a name="t5"></a>\*查看nohub命令下运行的所有后台进程：

jobs

## <a name="t7"></a><a name="t7"></a>\*查看后台运行的所有进程：

ps -aux

## <a name="t8"></a><a name="t8"></a>\*查看后台运行的所有python 进程：

ps aux |grep python或者ps -ef | grep python

## <a name="t10"></a><a name="t10"></a>\*删除进程

kill -9 \[进程id\]

-9 的意思是强制删除