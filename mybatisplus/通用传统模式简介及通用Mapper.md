# 2. 通用传统模式简介及通用Mapper

#### SSM传统编程模式：

> 接口中写抽象方法--》XML或注解写SQL--》Service中调用接口--》Controller中调用Service



### 通用Mapper：

**新增(Create)**

Mybatis-plus中的`BaseMapper`接口定义了很多通用的抽象方法，我们直接调用即可。

```java
@Autowired
private UserMapper userMapper;

@Test
public void insert(){
  User user = new User(9003L,"刘华强", 31, "liu@qq.com", 1001L, LocalDateTime.now());
  userMapper.insert(user);
}
```

