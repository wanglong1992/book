# oracle两种临时表的创建及使用方法

2017年08月23日 15:50:19

阅读数：7864

oracle数据库的临时表可以用来保存一个会话session的数据，或者一个事务中的数据。当查询语句非常复杂时，我们就可以创建一个临时表时保存查询结果，并进行一系列操作。

一、创建临时表

创建临时表有两种方式：
    1、会话级临时表  on commit delete rows;      当COMMIT的时候删除数据（默认情况）
    2、事务级临时表  on commit preserve rows;  当COMMIT的时候保留数据

1.会话级临时表

会话级临时表是指临时表中的数据只在会话生命周期之中存在，当用户退出会话结束的时候，[Oracle](http://www.2cto.com/database/Oracle/)自动清除临时表中数据。

执行commit或者rollback操作，表内数据依然存在，新建一个命令窗口（相当于开启了一个新的会话），表内的数据就查询不到了。

格式：

``

```plsql
Create Global Temporary Table Temp_Name



(



Col1 Type1,



Col2 Type2



...



)



On Commit Preserve Rows;
```

``

例子：

``

```plsql
create global temporary table temp_tb (col1 varchar(20)) on commit preserve rows;



insert into temp_tb values('test');



select * from temp_tb;
```

```plsql
Create Global Temporary Table Temp_Name



(



Col1 Type1,



Col2 Type2



...



)



On Commit Delete Rows;
```

例子

``

```plsql
create global temporary table temp_tb (col1 varchar(20)) on commit delete rows;



insert into  temp_tb values('test');



select * from  temp_tb;
CREATE GLOBAL TEMPORARY TABLE tmptable  



ON COMMIT PRESERVE ROWS   



AS  



SELECT *  



FROM tablename  
```