# 约束-自增约束-auto_increment

### 添加自增约束：

```mysql
-- 1.创建表时添加：
create table user3(id int primary key auto_increment,
                   name varchar(20));
                   
-- 2.通过ALTER语句添加：
alter table user3 modify id int auto_increment;
alter table user3 change id id int auto_increment;
```



*一张表只能有一个自增约束列，并且该列定义了约束（可以是primary key，可以是unique，也可以是foreign_key，但是不能是非空或检查约束）*

*自增长一般配合主键使用，并且只能在数字类型中使用*

### 删除自增约束：

```mysql
-- 通过ALTER语句删除：
alter table user3 modify id int; #方式1
alter table user3 change id id int; #方式2
```

