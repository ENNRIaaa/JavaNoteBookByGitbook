# 5.23 整合Mybatis框架

1. 引入依赖：

   ```xml
   <!-- mybatis-spring-boot-starter -->
   <dependency>
     <groupId>org.mybatis.spring.boot</groupId>
     <artifactId>mybatis-spring-boot-starter</artifactId>
     <version>2.1.3</version>
   </dependency>
   ```

2. 编写`UserMapper`接口：

   ```java
   @Mapper
   @Repository
   public interface UserMapper {
   
       List<User> queryUsersList();
   
       User queryUserById(Integer id);
   
       int addUser(User user);
   
       int updateUser(User user);
   
       int deleteUser(Integer id);
   }
   ```

   - `@Mapper`注解：说明这个接口是一个Mybatis映射器，也可以在Spring配置类中使用`@MapperScan("com.example.mapper")`注解来扫描映射器
   - `@Repository`：将映射器添加到容器，*可以不加这个注解*

3. 编写`UserMapper.xml`：

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.example.mapper.UserMapper">
   		<!--查询全部数据-->
       <select id="queryUsersList" resultType="user">
           select *
           from user1
       </select>
   </mapper>
   ```

4. 配置SpringBoot配置文件：

   ```yaml
   #mybatis配置
   mybatis:
     type-aliases-package: com.example.pojo
     mapper-locations: classpath:mybatis/mapper/*.xml
   ```

   设置实体类别名，将mybatis映射文件添加进来。

5. 编写控制类方法，进行测试：

   ```java
   @Controller
   @RequestMapping("/user")
   public class UserController {
   
       @Autowired
       private UserMapper userMapper;
   
       @GetMapping("queryUsers")
       @ResponseBody
       public List<User> queryUser(){
          return userMapper.queryUsersList();
       }
   }
   ```

   

