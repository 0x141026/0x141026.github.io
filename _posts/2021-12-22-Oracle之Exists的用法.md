---
id: 312
title: Oracle之Exists的用法
date: '2021-12-22T15:21:50+08:00'
author: Aaron
layout: post
guid: 'http://185.199.109.153/?p=312'
permalink: /2021/12/22/oracle%e4%b9%8bexists%e7%9a%84%e7%94%a8%e6%b3%95/
views:
    - '242'
seo_description_value:
    - oracle值exists
seo_keywords_value:
    - oracle值exists
categories:
    - Programming
tags:
    - oracle值exists
---

## （一）用Oracle Exists替换DISTINCT:

当提交一个包含一对多表信息(比如部门表和雇员表)的查询时，避免在SELECT子句中使用DISTINCT。一般能够考虑用Oracle EXIST替换，Oracle Exists使查询更为迅速，因为RDBMS核心模块将在子查询的条件一旦满足后，立即返回结果。  
例子：  
SELECT DISTINCT DEPT\_NO,DEPT\_NAME FROM DEPT D,EMP E WHERE D.DEPT\_NO = E.DEPT\_NO;

SELECT DEPT\_NO,DEPT\_NAME FROM DEPT D WHERE Exists (SELECT ‘X' FROM EMP E WHERE E.DEPT\_NO = D.DEPT\_NO);

## **（二）exists和in的效率问题:**

使用EXISTS，Oracle会首先检查主查询，然后运行子查询直到它找到第一个匹配项，这就节省了时间。Oracle在执行IN子查询时，首先执行 子查询，并将获得的结果列表存放在一个加了索引的临时表中。在执行子查询之前，系统先将主查询挂起，待子查询执行完毕，存放在临时表中以后再执行主查询。 这也就是使用EXISTS比使用IN通常查询速度快的原因。

1\) select \* from T1 where exists(select 1 from T2 where T1.a=T2.a) ;  
2\) select \* from T1 where T1.a in (select T2.a from T2) ;  
T1数据量小而T2数据量非常大时，T1&lt;&lt;T2时，1）的查询效率高。  
T1数据量非常大而T2数据量小时，T1&gt;&gt;T2 时，2）的查询效率高。

1)Select name from employee where name not in (select name from student);  
2)Select name from employee where not exists (select name from student);  
第一句SQL语句的执行效率不如第二句。

## 实例：

select \* from emp\_tax;

1\. 内表必须要和外表连接。

```sql
SELECT *
FROM emp_tax o
WHERE EXISTS (
	SELECT *
	FROM emp_tax i
	WHERE i.empno = o.empno
		AND i.empno < 5
);
```

2\. exists 适合外表的结果集小的情况。因为exists是对外表作loop，每次loop再对那表进行查询。  
当 exists 中的 where 后面条件为真的时候则把前面select 的内容显示出来(外表的select ).

## Tip:

in 是把外表和那表作hash join，而exists是对外表作loop，每次loop再对那表进行查询。  
这样的话，in适合内外表都很大的情况，exists适合外表结果集很小的情况。