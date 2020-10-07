# 约束-主键约束-primary_key

主键约束修饰的字段，不能重复且不能为null。

相当于唯一约束（unique）+ 非空约束（not null）。

**一张表最多只能有一个主键约束。**

### 添加主键约束：

```mysql
-- 1.创建表时为id字段添加主键约束
mysql> create table user1(id int primary key,
                          name varchar(20));
Query OK, 0 rows affected (0.02 sec)

mysql> desc user1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)



-- 2.通过ALTER语句添加：
alter table user1 modify id int primary key; #方式1
alter table user1 change id id int primary key; #方式2
alter table user1 add primary key(id); #方式3
alter table user1 add constraint primary key(id); #方式4
```



### 删除主键约束：

```mysql
-- 删除主键约束的方式
-- 通过ALTER语句删除：
alter table user1 drop primary key;

+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   |     | <null>  |       |
| name  | varchar(20) | YES  |     | <null>  |       |
+-------+-------------+------+-----+---------+-------+
```

*删除主键约束前，如果有自增约束需要先删除自增约束,如果不删除自增就无法删除主键约束。*