# 约束-非空约束-not_null

修饰的字段不能为空 NULL

### 添加非空约束

```mysql
-- 建表时直接添加
create table user9 (id int,name varchar(20) not null);

-- 通过ALTER语句添加：
alter table user9 modify name varchar(20) not null;

alter table user9 change name name varchar(20) not null;
```



### 删除非空约束

```mysql
-- 通过ALTER语句删除：
alter table user9 modify name varchar(20);

alter table user change name name varchar(20);
```

