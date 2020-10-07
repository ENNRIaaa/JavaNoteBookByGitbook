# 2. MySql 数据库使用

终端常用的命令：

##### 主键约束：

1. 建表时直接添加：

   ```mysql
   create table user (id int primary key,name varchar(20));
   ```

2. 通过alter语句添加：

   ```mysql
   alter table user add primary key (id);
   ```

   

