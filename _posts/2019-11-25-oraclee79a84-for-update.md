---
id: 226
title: 'Oracle的 for update'
date: '2019-11-25T16:48:11+08:00'
author: Aaron
layout: post
guid: 'http://47.101.191.3/?p=226'
permalink: /2019/11/25/oracle%e7%9a%84-for-update/
seo_description_value:
    - 'Oracle的 for update'
seo_keywords_value:
    - 'oracle;for update'
views:
    - '116'
categories:
    - Programming
tags:
    - 'oracle的for update'
---

## **pl/sql developer修改数据建议使用此种形式：**

1. select t.\*,t.rowid from table t;
2. select \* from table for update(一定记得commit提交，不然会引起很多锁表故障。)

## **使用场景:**

需要业务层面数据独占时，可以考虑使用for update。

场景上，比如火车票订票，在屏幕上显示有票，而真正进行出票时，需要重新确定一下这个数据没有被其他客户端修改。所以，在这个确认过程中，可以使用for update。