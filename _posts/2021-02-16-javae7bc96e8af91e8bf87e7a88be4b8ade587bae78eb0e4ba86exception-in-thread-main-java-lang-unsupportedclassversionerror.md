---
id: 230
title: 'java编译过程中出现了Exception in thread “main" java.lang.UnsupportedClassVersionError'
date: '2021-02-16T15:55:29+08:00'
author: Aaron
layout: post
guid: 'http://185.199.109.153/?p=230'
permalink: /2021/02/16/java%e7%bc%96%e8%af%91%e8%bf%87%e7%a8%8b%e4%b8%ad%e5%87%ba%e7%8e%b0%e4%ba%86exception-in-thread-main-java-lang-unsupportedclassversionerror/
views:
    - '166'
seo_description_value:
    - 'Exception in thread “main" java.lang.UnsupportedClassVersionError'
seo_keywords_value:
    - jvm
categories:
    - Programming
tags:
    - java
    - jvm
---

原因：这个问题是由较高版本的JDK编译(javac)的**java class文件或者jar文件**试图在较低版本的java(JVM)上运行产生的错误。比如说用jdk8环境编译生成的jar文件在java(jvm)6上运行就会出这样的错误。

**解决方案：将java(jvm)的版本和编译时的javac版本保持一致。**