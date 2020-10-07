# 数据表设计-第一范式1NF

```mysql
-- 第一范式 1NF （拆字段）

#数据表中的所有字段都是不可分割的原子值

create table student(
			id int primary key,
			name varchar(20),
			addreee varchar(30)
);

insert into student values(1,'张三','辽宁省大连市高新园区XXX号');
insert into student values(2,'李四','辽宁省沈阳市沈北新区XXX号');
insert into student values(3,'社会王','河北省北京市朝阳区XXX号');

+----+-----------+--------------------------------------+
| id | name      | addreee                              |
+----+-----------+--------------------------------------+
|  1 | 张三      | 辽宁省大连市高新园区XXX号            |
|  2 | 李四      | 辽宁省沈阳市沈北新区XXX号            |
|  3 | 社会王    | 河北省北京市朝阳区XXX号              |
+----+-----------+--------------------------------------+

-- 字段值还可以继续拆分的，就不满足第一范式

create table student2(
			id int primary key,
			name varchar(20),
			privence varchar(30),
  		city varchar(30),
  		details varchar(30)
);

insert into student2 values(1,'张三','辽宁省','大连市','高新园区XXX号');
insert into student2 values(2,'李四','辽宁省','沈阳市','沈北新区XXX号');
insert into student2 values(3,'社会王','河北省','北京市','朝阳区XXX号');

+----+-----------+-----------+-----------+--------------------+
| id | name      | privence  | city      | details            |
+----+-----------+-----------+-----------+--------------------+
|  1 | 张三      | 辽宁省    | 大连市    | 高新园区XXX号      |
|  2 | 李四      | 辽宁省    | 沈阳市    | 沈北新区XXX号      |
|  3 | 社会王    | 河北省    | 北京市    | 朝阳区XXX号        |
+----+-----------+-----------+-----------+--------------------+

-- 范式：设计得越详细，对于某些实际操作可能会更好，但是不一定都是好处
-- 数据表设计以实际开发需求为主，如果整个项目完全不需要去拆分字段，那就不需要参照范式
```

