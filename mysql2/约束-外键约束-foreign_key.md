# 约束-外键约束-foreign_key

涉及两个表：父表和子表

### 添加外键约束：

```mysql
-- 创建表时添加
mysql> create table students(
    -> id int primary key,
    -> name varchar(20),
    -> class_id int,
    -> constraint FK_students_classes foreign key (class_id) references classes(id)#创建表时添加外键约束
    -> );

-- 外键中的级联关系有以下几种情况：
#ON DELETE CASCADE 删除主表中的数据时，从表中的数据随之删除
#ON UPDATE CASCADE 更新主表中的数据时，从表中的数据随之更新
#ON DELETE SET NULL 删除主表中的数据时，从表中的数据置为空
#默认 删除主表中的数据前需先删除从表中的数据，否则主表数据不会被删除

mysql> create table students(
    -> id int primary key,
    -> name varchar(20),
    -> class_id int,
    -> constraint FK_students_classes foreign key(class_id) references classes(id) ON DELETE CASCADE#创建表时添加外键约束
    -> );

-- 通过alter语句添加
alter table user1 add constraint 外键（如FK_从表名_主表名） foreign key 从表名(字段) references 主表(字段);
```

示例：

创建两张表，一张班级表，一张学生表

```mysql
-- 创建classes表
create table classes( id int primary key,
    -> name varchar(20));
mysql> desc classes;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+

-- 创建students表
mysql> create table students(
    -> id int primary key,
    -> name varchar(20),
    -> class_id int,
    -> foreign key (class_id) references classes(id)#创建表时添加外键约束
    -> );
mysql> desc students2;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int(11)     | NO   | PRI | NULL    |       |
| name     | varchar(20) | YES  |     | NULL    |       |
| class_id | int(11)     | YES  | MUL | NULL    |       |
+----------+-------------+------+-----+---------+-------+
-- 添加班级
mysql> insert into classes values (1,'一班');
mysql> insert into classes values (2,'二班');
mysql> insert into classes values (3,'三班');
mysql> insert into classes values (4,'四班');
mysql> select * from classes;
+----+--------+
| id | name   |
+----+--------+
|  1 | 一班   |
|  2 | 二班   |
|  3 | 三班   |
|  4 | 四班   |
+----+--------+
-- 添加学生1
mysql> insert into students values(10001,'张三',1);
-- 添加学生，class_id=5
mysql> insert into students values(10002,'张三',5);
-- 报错
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`test`.`students`, CONSTRAINT `fk_students_classes` FOREIGN KEY (`class_id`) REFERENCES `classes` (`id`))
```



### 删除外键约束：

```mysql
alter table user1 drop foreign key 外键（FK_从表_主表）;
```

