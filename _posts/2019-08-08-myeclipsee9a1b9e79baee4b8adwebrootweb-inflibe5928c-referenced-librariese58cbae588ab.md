---
id: 235
title: 'MyEclipse项目中WebRoot\web-inf\lib和 Referenced Libraries区别'
date: '2019-08-08T20:53:15+08:00'
author: Aaron
layout: post
guid: 'http://47.101.191.3/?p=235'
permalink: /2019/08/08/myeclipse%e9%a1%b9%e7%9b%ae%e4%b8%adwebrootweb-inflib%e5%92%8c-referenced-libraries%e5%8c%ba%e5%88%ab/
views:
    - '175'
seo_description_value:
    - 'MyEclipse项目中WebRoot\web-inf\lib和 Referenced Libraries区别'
seo_keywords_value:
    - 'java library'
categories:
    - 未分类
tags:
    - java依赖库
---

Referenced Libraries是**编译环境下使用的JAR包**,所谓编译环境下使用的JAR包, 就是说你在Eclipse中进行源文件的编写的时候,所需要引用到的类都从Referenced Libraries这个集合中的JAR包中拿;

/web-inf/lib中的JAR包是**运行时环境下使用的JAR包**,所谓运行时环境下使用的JAR包,就是说你在运行你的项目的时候所需要使用的JAR包的集合。

  
放到lib下也是一个好习惯，引用其它位置的jar【通常某些同学喜欢用myeclipse自动添加对struts、spring、hibernate的支持】，使用这种方式，很容易造成jar包冲突、缺失的问题，尤其是团队协作的情况下，*如果你引用了本地硬盘上的某个jar，提交了.classpath文件到svn，别人检出后，就会报错*，因为他的硬盘上的同一位置没有这个jar,而如果你放到lib下，再提交，检出后他的lib下是有这个jar的，因为lib是工程的一部分。

**结论：**所以最好直接将jar包复制粘贴到在WebContent-&gt;WEB-INF-&gt;lib下即可。另外在WebContent-&gt;WEB-INF-&gt;lib下的jar包路径都会写在项目名/.classpath文件中

.开头的配置文件在Navigator视图下可以看到