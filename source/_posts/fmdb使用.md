title: FMDB使用
date: 2015-01-10 18:53:12
tags:
---

#FMDB
===

1. FMDB的背景：基于sqlite3封装的第三方库，而sqlite3属于轻量级数据库
  

2.基本介绍

- 数据库中数据类型：因为sqlite3采用的动态数据类型，所以从数据库中取值需要我们进行转码

	数据类型   |存储的数据
	-------   |----------- 
	BLOB      |图片、音频
	TEXT      |文本
	INTEGER   |整形
	BOOLEAN   |布尔（会转化为0，1存储）
	DATE	  |日期
	
- 从数据库中取出数据：
  根据你在存在数据库中的类型，来使用对应的取值方法
  
- 表间数据操作

-  
  
- 执行语句：增删改查
   
      增：1.Insert语句INSERT INTO TABLE_NAME VALUES 
      (value1,value2,value3,...valueN)与表中一一对应
      	  2.INSERT INTO TABLE_NAME (column1, column2, 
      	  column3,...columnN)]VALUES (value1, value2, 
      	  value3,...valueN);给指定行中插入数据
      删：Delete语句
      DELETE FROM table_name WHERE [条件];
      改：update语句
      UPDATE table_name  SET column1 = value1, column2 = 
      value2...., columnN = valueN WHERE [condition];
      查：Selecte语句
      SELECT column1, column2, columnN FROM table_name

-  基于FMDB中的多线程FMDB

3.执行过程中，需要注意的事项：

