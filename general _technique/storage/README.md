# 持久存储

## 沙盒
- 沙盒下三个文件夹
    - Documents: 存放应用程序的数据 (苹果建议将程序中建立的或在程序中浏览到的文件数据保存在该目录下，iTunes备份和恢复的时候会包括此目录)
    - Library: 存储程序的默认设置或其它状态信息
    - tmp: 应用程序存储临时文件

## 数据库

##### 什么是SQL

sql是数据库查询语言，适用于访问和处理数据库的标准的计算机语言。
  -  SQL 面向数据库执行查询
  -  SQL 可从数据库取回数据
  -  SQL 可在数据库中插入新的记录
  -  SQL 可更新数据库中的数据
  -  SQL 可从数据库删除记录
  -  SQL 可创建新数据库
  -  SQL 可在数据库中创建新表
  -  SQL 可在数据库中创建存储过程
  -  SQL 可在数据库中创建视图
  -  SQL 可以设置表、存储过程和视图的权限

##### SQL语句

下面的语句从表中选取 LastName 列的数据：

- SELECT LastName FROM Persons
- 一定要记住，SQL 对大小写不敏感
- ; 每条SQL命令后添加分号
- 部分指令
   - SELECT - 从数据库表中获取数据
   - UPDATE - 更新数据库表中的数据
   - DELETE - 从数据库表中删除数据
   - INSERT INTO - 向数据库表中插入数据
   -
   - CREATE DATABASE - 创建新数据库
   - ALTER DATABASE - 修改数据库
   - CREATE TABLE - 创建新表
   - ALTER TABLE - 变更（改变）数据库表
   - DROP TABLE - 删除表
   - CREATE INDEX - 创建索引（搜索键）
   - DROP INDEX - 删除索引

#### SELECT语句

语句用于从表中选取数据，结果被存储在一个结果表中

1. 语法：
    - SELECT 列名称 FROM 表名称
    - SELECT * FROM 表名称
    - 注释：SQL 语句对大小写不敏感。SELECT 等效于 select。

![](images/Snip20161215_1.png)

####  SELECT DISTINCT 语句

在表中，可能会包含重复值。这并不成问题，不过，有时您也许希望仅仅列出不同（distinct）的值。

关键词 DISTINCT 用于返回唯一不同的值。

1. 语法
    - SELECT DISTINCT 列名称 FROM 表名称

![](images/Snip20161215_2.png)

#### WHERE子句

如需有条件地从表中选取数据，可将 WHERE 子句添加到 SELECT 语句。

1. 语法:
    - SELECT 列名称 FROM 表名称 WHERE 列 运算符 值

![](images/Snip20161215_3.png)
![](images/Snip20161215_5.png)

#### AND & OR 运算符

AND 和 OR 运算符用于基于一个以上的条件对记录进行过滤。

1. AND 和 OR 运算符
    - AND 和 OR 可在 WHERE 子语句中把两个或多个条件结合起来
    - 如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。
    - 如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。

![](images/Snip20161215_6.png)
![](images/Snip20161215_7.png)

#### ORDER BY

ORDER BY 语句用于对结果集进行排序

1. 语法
    - ORDER BY 语句用于根据指定的列对结果集进行排序
    - ORDER BY 语句默认按照升序对记录进行排序
    - 如果您希望按照降序对记录进行排序，可以使用 DESC 关键字

![](images/Snip20161215_8.png)
![](images/Snip20161215_9.png)
![](images/Snip20161215_10.png)

#### INSERT INTO

![](images/Snip20161215_11.png)
![](images/Snip20161215_12.png)

#### UPDATE

![](images/Snip20161215_13.png)

#### DELETE

![](images/Snip20161215_15.png)

#### TOP
![](images/Snip20161215_20.png)
![](images/Snip20161215_21.png)

#### LIKE
![](images/Snip20161215_22.png)
![](images/Snip20161215_23.png)

#### 通配符

![](images/Snip20161215_25.png)
![](images/Snip20161215_26.png)
![](images/Snip20161215_27.png)

#### IN 操作符

![](images/Snip20161215_28.png)

#### BETWEEN操作符
![](images/Snip20161215_29.png)
![](images/Snip20161215_30.png)

#### Alias（别名）
![](images/Snip20161215_32.png)
![](images/Snip20161215_33.png)

#### JOIN
![](images/Snip20161215_35.png)
![](images/Snip20161215_36.png)
![](images/Snip20161215_37.png)

#### INNER JOIN
![](images/Snip20161215_38.png)
![](images/Snip20161215_39.png)

#### LEFT JOIN
![](images/Snip20161215_40.png)
![](images/Snip20161215_41.png)

#### RIGHT JOIN
![](images/Snip20161215_42.png)
![](images/Snip20161215_43.png)

#### FULL JOIN
![](images/Snip20161215_44.png)
![](images/Snip20161215_45.png)

#### UNION
![](images/Snip20161215_46.png)
![](images/Snip20161215_47.png)
![](images/Snip20161215_48.png)

#### SELECT INTO

![](images/Snip20161215_49.png)
![](images/Snip20161215_51.png)

#### CREATE DATAEBASE 语句

![](images/Snip20161215_52.png)

#### CREATE TABLE 语句
![](images/Snip20161215_53.png)
![](images/Snip20161215_54.png)

#### 约束 (Constraints)
![](images/Snip20161215_55.png)

#### NOT NULL 约束
![](images/Snip20161215_56.png)

#### UNIQUE 约束
![](images/Snip20161215_57.png)
![](images/Snip20161215_58.png)

#### PRIMARY KEY 约束
![](images/Snip20161216_1.png)
![](images/Snip20161216_2.png)

#### FOREIGN KEY 约束
![](images/Snip20161216_3.png)
![](images/Snip20161216_4.png)
![](images/Snip20161216_5.png)

#### CHECK 约束
![](images/Snip20161216_6.png)
![](images/Snip20161216_7.png)

#### DEFAULT 约束
![](images/Snip20161216_10.png)
![](images/Snip20161216_12.png)

#### CREATE INDEX 语句
![](images/Snip20161216_13.png)

#### 撤销索引、表以及数据库
![](images/Snip20161216_14.png)

#### ALTER TABLE 语句
![](images/Snip20161216_15.png)
![](images/Snip20161216_16.png)

#### AUTO INCREMENT 字段
![](images/Snip20161216_17.png)
![](images/Snip20161216_18.png)
![](images/Snip20161216_19.png)

#### VIEW（视图）
![](images/Snip20161216_20.png)
![](images/Snip20161216_21.png)
![](images/Snip20161216_22.png)

#### Date 函数
![](images/Snip20161216_23.png)
![](images/Snip20161216_24.png)
![](images/Snip20161216_25.png)

#### NULL 值
![](images/Snip20161216_26.png)
![](images/Snip20161216_27.png)

#### NULL 函数
![](images/Snip20161216_28.png)
![](images/Snip20161216_29.png)

#### 数据类型
![](images/Snip20161216_30.png)
![](images/Snip20161216_31.png)
![](images/Snip20161216_32.png)
![](images/Snip20161216_33.png)
![](images/Snip20161216_34.png)
![](images/Snip20161216_35.png)

#### 服务器 - RDBMS
![](images/Snip20161216_36.png)
