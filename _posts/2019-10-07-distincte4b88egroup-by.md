---
id: 236
title: 'distinct与group by'
date: '2019-10-07T11:01:48+08:00'
author: Aaron
layout: post
guid: 'http://47.101.191.3/?p=236'
permalink: /2019/10/07/distinct%e4%b8%8egroup-by/
seo_description_value:
    - 'distinct与group by'
seo_keywords_value:
    - sql语句
views:
    - '88'
categories:
    - Programming
tags:
    - sql语句
---

1. 有时候如果只是向查询不重复的记录，使用distinct即可，一个单词解决
2. 另外distinct必须放在最前面
3. distinct a, b, c表示同时作用与三列，而不是作用于a

- - - - - -

select a.id,a.spmc,b.jg 凌家塘,c.jg 镇江智慧物价网,d.jg 常州价格通网菜场,e.jg 常州价格通网菜场

from spdz a left join (select jg, spmc from spjg where zqpc='191106173823' and sply='凌家塘') b  
on a.ljt=b.spmc left join (select jg, spmc from spjg where zqpc='191106173823' and sply='镇江智慧物价网') c  
on a.zjwjw=c.spmc left join (select jg, spmc from spjg where zqpc='191106173823' and sply='常州价格通网菜场') d  
on a.czjgt=d.spmc left join (select jg, spmc from spjg where zqpc='191106173823' and sply='常州价格通网菜场') e  
on a.czjgt=e.spmc group by b.jg,c.jg,d.jg,e.jg,a.spmc,a.id order by a.id

**等价于**

select distinct a.id,a.spmc,b.jg 凌家塘,c.jg 镇江智慧物价网,d.jg 常州价格通网菜场,e.jg 常州价格通网菜场

from spdz a left join (select jg, spmc from spjg where zqpc='191106173823' and sply='凌家塘') b  
on a.ljt=b.spmc left join (select jg, spmc from spjg where zqpc='191106173823' and sply='镇江智慧物价网') c  
on a.zjwjw=c.spmc left join (select jg, spmc from spjg where zqpc='191106173823' and sply='常州价格通网菜场') d  
on a.czjgt=d.spmc left join (select jg, spmc from spjg where zqpc='191106173823' and sply='常州价格通网菜场') e  
on a.czjgt=e.spmc