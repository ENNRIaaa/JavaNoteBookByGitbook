# 5.21 整合JDBC

对于数据访问层，无论是SQL还是NOSQL，SpringBoot底层都是采用Spring Data的方式进行统一处理。

SpringBoot底层都是采用Spring Data的方式进行统一处理各种数据库，Spring Data也是Spring中与SpringBoot、Spring Cloud等齐名的项目。



#### SpringBoot使用jdbc操作数据库

1. 创建SpringBoot项目，并添加启动器：

   ```xml
   <!--jdbc-->
   <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-jdbc</artifactId>
   </dependency>
   
   <!--mysql驱动-->
   <dependency>
     <groupId>mysql</groupId>
     <artifactId>mysql-connector-java</artifactId>
     <scope>runtime</scope>
   </dependency>
   
   <!--spring mvc-->
   <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

2. 在`application.yml`中配置数据源：

   ```yaml
   # mysql数据源
   spring:
     datasource:
       driver-class-name: com.mysql.cj.jdbc.Driver
       url: jdbc:mysql://localhost:3306/neu_javaweb
       username: root
       password: 12345678
   ```

3. 获取连接对象：

   打印输出数据源DataSource对象和Connection对象：

   ```java
   @Autowired
   private DataSource dataSource;
   
   @Test
   void contextLoads() throws SQLException {
   
     System.out.println(dataSource.getClass());
   
     //获取连接对象
     Connection conn = dataSource.getConnection();
     System.out.println(conn);
   }
   ```

   > class com.zaxxer.hikari.HikariDataSource
   >
   > HikariProxyConnection@1412752396 wrapping com.mysql.cj.jdbc.ConnectionImpl@3b48e183

   *SpringBoot默认的连接池HikariDataSource*



#### 使用JdbcTemplate

`JdbcTemplate`是Spring的一个操作数据库的工具类，在学习JDBC的时候使用过。https://javabook.shiguangping.com/mysql3/SpringJDBC.html

1. 创建一个包controller，创建JdbcController类：

   ```java
   @Controller
   public class JdbcController {
   
       @Autowired
       private JdbcTemplate jdbcTemplate;
   
       /**
        * 查询数据库的所有数据
        */
       @RequestMapping("/queryUsers")
       @ResponseBody
       public List<Map<String, Object>> userList() {
           String sql = "select * from user1";
           return jdbcTemplate.queryForList(sql);
       }
   }
   ```

   *JdbcTemplate查询数据库非常方便，可以直接将查询数据封装到List集合中，也可以直接封装成实体类对象。*

