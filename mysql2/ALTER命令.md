# ALTER命令-菜鸟教程

当需要修改数据表名或者修改数据表字段时，就需要使用到MySQL ALTER命令。

先创建一张名为 `testalter_tbl`的表：

```mysql
mysql> create database RUNOOB;
Query OK, 1 row affected
Time: 0.006s
mysql> use RUNOOB;
You are now connected to database "RUNOOB" as user "root"
Time: 0.001s
-- 创建名为 testalter_tbl的表
mysql> create table testalter_tbl(
                          -> i int,
                          -> c char(1)
                          -> );
Query OK, 0 rows affected
-- 查看表结构
mysql> desc testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| i     | int(11) | YES  |     | <null>  |       |
| c     | char(1) | YES  |     | <null>  |       |
+-------+---------+------+-----+---------+-------+
```



### 删除、添加、修改表字段

```mysql
-- 删除以上创建表的i字段
mysql> alter table testalter_tbl drop i;
mysql> desc testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| c     | char(1) | YES  |     | <null>  |       |
+-------+---------+------+-----+---------+-------+

-- 使用add从句添加字段
mysql> alter table testalter_tbl add i int;
mysql> desc testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| c     | char(1) | YES  |     | NULL    |       |
| i     | int(11) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.01 sec)

-- 如果需要制定新增字段的位置，可以使用FIRST关键字（设定位于第一列），AFTER字段名（设定位于某个某一字段之后）
-- 先删除i
mysql> alter table testalter_tbl drop i;
-- 使用FIRST字段添加i
mysql> alter table testalter_tbl add i int first;


mysql> desc testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| i     | int(11) | YES  |     | NULL    |       |
| c     | char(1) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+


-- 删除i，使用AFTER在c字段后面添加i
mysql> alter table testalter_tbl drop i;
mysql> alter table testalter_tbl add i int after c;
mysql> desc testalter_tbl;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| c     | char(1) | YES  |     | NULL    |       |
| i     | int(11) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+

-- FIRST和AFTER关键字可用于ADD与MODIFY子句，所以如果想重置数据表字段的位置就需要先使用DROP删除字段然后使用ADD来添加字段并设置位置。
```



### 修改字段类型及名称

```mysql
-- 如果需要修改字段类型及名称，可以在ALTER命令中使用MODIFY或CHANGE子句。
-- 把字段c类型从char(1)改成char(10):
mysql> alter table testalter_tbl modify c char(10);
mysql> desc testalter_tbl;
+-------+----------+------+-----+---------+-------+
| Field | Type     | Null | Key | Default | Extra |
+-------+----------+------+-----+---------+-------+
| c     | char(10) | YES  |     | NULL    |       |
| i     | int(11)  | YES  |     | NULL    |       |
+-------+----------+------+-----+---------+-------+

-- 使用CHANGE子句，语法有很大不同。在CHANGE关键字后，紧跟着要修改的字段名，然后指定新字段的名称及类型：
-- 使用CHANGE子句把字段改成j类型为BIGINT：
mysql> alter table testalter_tbl change i j bigint;
mysql> desc testalter_tbl;
+-------+------------+------+-----+---------+-------+
| Field | Type       | Null | Key | Default | Extra |
+-------+------------+------+-----+---------+-------+
| c     | char(10)   | YES  |     | NULL    |       |
| j     | bigint(20) | YES  |     | NULL    |       |
+-------+------------+------+-----+---------+-------+

-- 再把j改回int
mysql> alter table testalter_tbl change j j int;
mysql> desc testalter_tbl;
+-------+----------+------+-----+---------+-------+
| Field | Type     | Null | Key | Default | Extra |
+-------+----------+------+-----+---------+-------+
| c     | char(10) | YES  |     | NULL    |       |
| j     | int(11)  | YES  |     | NULL    |       |
+-------+----------+------+-----+---------+-------+
```



### ALTER TABLE对Null值和默认值的影响

```mysql
-- 当修改字段是，可以指定是否包含值或者是否设置默认值
-- 指定字段j为NOT NULL且默认值为100：
mysql> alter table testalter_tbl modify j bigint not null default 100;
mysql> desc testalter_tbl;
+-------+------------+------+-----+---------+-------+
| Field | Type       | Null | Key | Default | Extra |
+-------+------------+------+-----+---------+-------+
| c     | char(10)   | YES  |     | NULL    |       |
| j     | bigint(20) | NO   |     | 100     |       |
+-------+------------+------+-----+---------+-------+
-- 如果不设置控制，MySQL会自动设置该字段为NULL

-- 修改字段默认值：
-- 将字段j默认值修改成1000：
mysql> alter table testalter_tbl alter j set default 1000;
mysql> desc testalter_tbl;
+-------+------------+------+-----+---------+-------+
| Field | Type       | Null | Key | Default | Extra |
+-------+------------+------+-----+---------+-------+
| c     | char(10)   | YES  |     | NULL    |       |
| j     | bigint(20) | NO   |     | 1000    |       |
+-------+------------+------+-----+---------+-------+

-- 使用drop语句删除字段默认值
mysql> alter table testalter_tbl alter i drop default;
mysql> desc testalter_tbl;
+-------+------------+------+-----+---------+-------+
| Field | Type       | Null | Key | Default | Extra |
+-------+------------+------+-----+---------+-------+
| c     | char(10)   | YES  |     | NULL    |       |
| j     | bigint(20) | NO   |     | NULL    |       |
+-------+------------+------+-----+---------+-------+
```



### 修改表名

```mysql
-- 可以在ALTER TABLE语句中使用RENAME子句修改表名：
mysql> alter table testalter_tbl rename alter_tbl;
mysql> show tables;
+------------------+
| Tables_in_runoob |
+------------------+
| alter_tbl        |
+------------------+
```

