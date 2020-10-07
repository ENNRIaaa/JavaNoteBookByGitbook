# 数据表设计-第一范式3NF

```mysql
-- 第二范式 3NF
-- 必须满足第二范式，除开主键列外的其他列之间不能有传递依赖。

create table myorder(
			order_id int primary key,
  		pruduct_id int,
  		customer_id int,
  		customer_phone varchar(15) #假设customer_phone有对order_id的依赖，满足第二范式要求。但它也依赖于customer_id，所以不满足第三范式。
);

create table customer(
			id int primary key,
  		name varchar(20),
  		phone varchar(15)# 应该把customer_phone放到customer表中
);
```

