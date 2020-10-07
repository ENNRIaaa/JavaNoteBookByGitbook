# 5.33 Shiro整合Mybatis

1. 添加依赖：

   ```xml
   <!--mysql驱动-->
   <dependency>
     <groupId>mysql</groupId>
     <artifactId>mysql-connector-java</artifactId>
   </dependency>
   <!--druid数据源-->
   <dependency>
     <groupId>com.alibaba</groupId>
     <artifactId>druid</artifactId>
     <version>1.1.22</version>
   </dependency>
   <!--mybatis-springboot整合-->
   <dependency>
     <groupId>org.mybatis.spring.boot</groupId>
     <artifactId>mybatis-spring-boot-starter</artifactId>
     <version>2.1.3</version>
   </dependency>
   <!--log4j-->
   <dependency>
     <groupId>log4j</groupId>
     <artifactId>log4j</artifactId>
     <version>1.2.17</version>
   </dependency>
   ```

2. 配置`application.yml`

   ```yaml
   # 配置数据源
   spring:
     datasource:
       type: com.alibaba.druid.pool.DruidDataSource
       username: root
       password: 12345678
       driver-class-name: com.mysql.cj.jdbc.Driver
       url: jdbc:mysql://localhost:3306/neu_javaweb
       
   # 配置mybatis
   mybatis:
     type-aliases-package: com.example.pojo
     mapper-locations: classpath:mybatis/mapper/*.xml
   ```

3. 定义实体类：

   ```java
   @Data
   @AllArgsConstructor
   @NoArgsConstructor
   public class User {
       private Integer id;
       private String username;
       private String password;
   }
   ```

4. UserMapper接口：

   ```java
   @Mapper
   @Repository
   public interface UserMapper {
       /**
        * 通过用户名获取User数据
        * @param username
        * @return
        */
       User queryUserByName(String username);
   }
   ```

5. UserMapper.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.example.mapper.UserMapper">
   
       <select id="queryUserByName" parameterType="string" resultType="user">
           select * from user1 where username = #{username}
       </select>
   </mapper>
   ```

   ***到这为止，mybatis环境搭建完成***

6. `UserRealm`类中通过表单提交的用户名从数据库获取User数据，再认证：

   - 如果获取的User为null，说明登陆的用户名不存在，return null，抛出UnknownAccountException异常；

   - 如果获取的User不为null，继续验证密码

   ```java
   @Autowired
   private UserService userService;
   
   @Override
   protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
     // 通过前端提交的用户名从数据库获取User数据
     User user = userService.queryUserByName((String) token.getPrincipal());
   
     // 如果user为null，说明用户名不存在，返回null抛出异常UnknownAccountException
     if (user == null) {
       return null;
     }
     // 反之，返回SimpleAuthenticationInfo，校验密码
     return new SimpleAuthenticationInfo("", user.getPassword(), "");
   }
   ```

   