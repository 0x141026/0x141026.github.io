---
id: 310
title: 'java编译过程中出现了Exception in thread “main" java.lang.UnsupportedClassVersionError'
date: '2021-12-22T14:39:07+08:00'
author: Aaron
layout: revision
guid: 'http://47.101.191.3/?p=310'
permalink: '/?p=310'
---

原因：这个问题是由较高版本的JDK编译(javac)的**java class文件或者jar文件**试图在较低版本的java(JVM)上运行产生的错误。比如说用jdk8环境编译生成的jar文件在java(jvm)6上运行就会出这样的错误。

**解决方案：将java(jvm)的版本和编译时的javac版本保持一致。**