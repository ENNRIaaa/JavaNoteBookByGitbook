# 约束-默认约束-default

当我们插入字段值的时候，如果没有传值，就会使用默认值。



### 添加默认约束：

```mysql
-- 在创建表时添加
-- 通过ALTER语句添加：
alter table user1 modify id int default 10; #方式1
alter table user1 change id id int default 10; #方式2
```



### 删除默认约束：

```mysql
-- 通过ALTER语句删除：
alter table user1 modify id int;
alter table user1 change id id int;
```



示例：

```mysql
-- 创建表user10
mysql> create table user10( id int, name varchar(20), age int default 10);
Query OK, 0 rows affected (0.10 sec)
-- age设置了默认值
mysql> desc user10;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int(11)     | YES  |     | 10      |       |
+-------+-------------+------+-----+---------+-------+
-- 只插入id和name
mysql> insert into user10(id,name) values(1,'张三');
Query OK, 1 row affected (0.02 sec)
-- age默认为10
mysql> select * from user10;
+------+--------+------+
| id   | name   | age  |
+------+--------+------+
|    1 | 张三   |   10 |
+------+--------+------+
```



