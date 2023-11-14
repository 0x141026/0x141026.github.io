---
id: 221
title: sqlserver不同版本之间数据库的还原方法
date: '2019-09-27T14:05:54+08:00'
author: Aaron
layout: post
guid: 'http://185.199.109.153/?p=221'
permalink: /2019/09/27/sqlserver%e4%b8%8d%e5%90%8c%e7%89%88%e6%9c%ac%e4%b9%8b%e9%97%b4%e6%95%b0%e6%8d%ae%e5%ba%93%e7%9a%84%e8%bf%98%e5%8e%9f%e6%96%b9%e6%b3%95/
seo_description_value:
    - 'sqlserver不同版本之间的还原 sqlserver不同版本之间的还原'
seo_keywords_value:
    - ' sqlserver，不同版本，数据库还原还原'
views:
    - '178'
categories:
    - Programming
tags:
    - sqlserver不同版本之间的还原
---

## **一、相同版本之间还原**

1.在一台数据库上备份bak文件直接还原到另外一台数据库上

2.如果上述出现问题，先新建一个数据库，然后则执行如下代码还原（修改红色部分为bak文件在PC上的位置）：

<div class="cnblogs_code">```
restore database htzjpic from disk='E:\htzjpic.bak'with RECOVERY,REPLACE, CONTINUE_AFTER_ERROR,
move 'htzjpic' to 'E:\Program Files (x86)\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\htzjpic.mdf',
move 'htzjpic_log' to 'E:\Program Files (x86)\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\htzjpic_log.ldf'
```

</div>## **二、低版本还原到高版本**

直接将低版本的数据库bak文件还原到高版本的数据库中

## **三、高版本还原到低版本**

首先，右击高版本的数据库生成脚本，点击高级将版本号选择对应的低版本，并点击编写的数据类型选择为：架构和数据，最后点确定等待生成脚本文件。

然后，将脚本文件拷贝到低版本数据库的电脑，打开该脚本文件，**先新建同名的数据库**再F5执行。

参考：[https://blog.csdn.net/weixin\_34177064/article/details/94721817](https://blog.csdn.net/weixin_34177064/article/details/94721817)

### 凡是出现：介质簇的结构不正确的错误，就表示高版本的bak在向低版本的数据库操作

## PS：从备份文件bak中识别SQL Server版本的sql语句

<div class="cnblogs_code">```
1 RESTORE HEADERONLY FROM DISK = N'D:\SQLSERVER_DATA\备份文件\XXXX.bak'
```

</div>参考：<https://www.cnblogs.com/Rawls/p/10726010.html>