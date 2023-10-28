---
id: 309
title: 'windows下git bash命令行记住命令案上下键搜索'
date: '2021-12-16T09:23:23+08:00'
author: Aaron
layout: post
guid: 'http://47.101.191.3/?p=309'
permalink: /2021/12/16/windows%e4%b8%8bgit-bash%e5%91%bd%e4%bb%a4%e8%a1%8c%e8%ae%b0%e4%bd%8f%e5%91%bd%e4%bb%a4%e6%a1%88%e4%b8%8a%e4%b8%8b%e9%94%ae%e6%90%9c%e7%b4%a2/
views:
    - '215'
seo_description_value:
    - bash配置
categories:
    - Programming
tags:
    - bash
---

1、在家目录配置或者新增.inputrc文件

2、编辑.inputrc文件，添加如下代码：

> "\\e\[A": history-search-backward  
> "\\e\[B": history-search-forward  
> set show-all-if-ambiguous on  
> set completion-ignore-case on