# 数据表设计-第一范式2NF

```mysql
-- 第二范式 2NF （拆表）
-- 必须是满足第一范式的前提下，第二范式要求，除主键外的每一列都必须完全依赖主键。
-- 如果要出现不完全依赖，只可能发生在联合主键情况下。

-- 订单表
create table myorder(
			product_id int,
			customer_id int,
  		product_name varchar(20),
  		customer_name varchar(20).
  		primary key(product_id,customer_id)
);

-- 问题？
-- 除主键外的其他列，只依赖于主键的部分字段。（不满足第二范式）
-- 拆表
create table myorder(
			order_id int primary key,
  		pruduct_id int,
  		customer_id int
);

create table product(
			id int primary key,
  		name varchar(20)
);

create table customer(
			id int primary key,
  		name varchar(20)
);

-- 拆分成三个表之后，满足第二范式
```

