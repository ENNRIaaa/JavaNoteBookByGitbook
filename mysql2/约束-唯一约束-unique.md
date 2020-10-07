# 约束-唯一约束-unique

约束字段的值不可以重复。

### 添加唯一约束：

```mysql
-- 1.可以在创建表时直接添加
-- 2.通过ALTER语句：
alter table user5 add unique (name); #方式1
alter table user5 add unique key (name); #方式2
alter table user5 modify name varchar(20) unique; #方式3
alter table user5 change name name varchar(20) unique; #方式4
alter table user5 add constraint unique (name); #方式5
alter table user5 add constraint unique key(name); #方式6
```



*注意：联合唯一约束，即多个字段设置了唯一约束，多个字段的值相加不能相同；有一个字段不同即可插入。*

### 删除唯一约束

```mysql
-- 删除唯一约束
alter table user drop index name;
```



