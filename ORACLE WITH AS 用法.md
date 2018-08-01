```plsql
ORACLE WITH AS 用法
Posted on 2012-10-11 15:05 宽田 阅读(63957) 评论(0) 编辑 收藏
语法：

with tempName as (select ....)
select ...
 

 

例：现在要从1-19中得到11-14。一般的sql如下：

复制代码
select * from
(
            --模拟生一个20行的数据
             SELECT LEVEL AS lv
               FROM DUAL
         CONNECT BY LEVEL < 20
) tt
 WHERE tt.lv > 10 AND tt.lv < 15
复制代码
 

使用With as 的SQL为：

复制代码
with TT as(
                --模拟生一个20行的数据
                 SELECT LEVEL AS lv
                 FROM DUAL
                CONNECT BY LEVEL < 20
             ) 
select lv from TT
WHERE lv > 10 AND lv < 15
复制代码
 

With查询语句不是以select开始的，而是以“WITH”关键字开头
    可认为在真正进行查询之前预先构造了一个临时表TT，之后便可多次使用它做进一步的分析和处理

WITH Clause方法的优点
     增加了SQL的易读性，如果构造了多个子查询，结构会更清晰；更重要的是：“一次分析，多次使用”，这也是为什么会提供性能的地方，达到了“少读”的目标。

     第一种使用子查询的方法表被扫描了两次，而使用WITH Clause方法，表仅被扫描一次。这样可以大大的提高数据分析和查询的效率。

     另外，观察WITH Clause方法执行计划，其中“SYS_TEMP_XXXX”便是在运行过程中构造的中间统计结果临时表。
```