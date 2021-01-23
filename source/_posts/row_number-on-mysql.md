---
title: 如何在MySQL中实现row_number函数
date: 2015-11-29 16:22:16
tags: [MySQL]
---
很久之前给自己挖的坑，现在来把它补完。
MySQL的统计函数比较稀缺，很多经典的统计函数如row_number这样的函数在MySQL是没有的，不确定最新版本会不会增加。
为了实现这个功能，需要在查询中启用临时变量。
比如对这张Employee表加上行号：
| Id  | Salary |
| :-- | :----- |
| 1   | 100    |
| 2   | 200    |
| 3   | 300    |

代码如下：
```sql
SET @row_number = 0;
 
SELECT 
    (@row_number:=@row_number + 1) AS num, id, salary
FROM
    employee
LIMIT 10;
```

也可以这样写：
```sql
SELECT 
    (@row_number:=@row_number + 1) AS num, id, salary
FROM
    employee,(SELECT @row_number:=0) AS t
LIMIT 10;
```

参考文章：
[https://segmentfault.com/a/1190000004566152](https://segmentfault.com/a/1190000004566152)
