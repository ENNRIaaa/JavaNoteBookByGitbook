# 5.22 整合Druid数据源

#### 添加Druid数据源：

1. 添加依赖坐标：

   ```xml
   <dependency>
     <groupId>com.alibaba</groupId>
     <artifactId>druid</artifactId>
     <version>1.1.22</version>
   </dependency>
   ```

2. ymal中设置type属性：

   ```yaml
   # mysql数据源
   spring:
     datasource:
       driver-class-name: com.mysql.cj.jdbc.Driver
       url: jdbc:mysql://localhost:3306/neu_javaweb
       username: root
       password: 12345678
       type: com.alibaba.druid.pool.DruidDataSource
       # 初始化大小，最小，最大
       initialSize: 5
       minIdle: 5
       maxActive: 20
       # 配置获取连接等待超时的时间(毫秒)
       maxWait: 3000
       # 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒
       timeBetweenEvictionRunsMillis: 60000
       # 配置有一个连接在连接池中的最小生存时间，单位是毫秒
       minEvictableIdleTimeMillis: 300000
       validationQuery: SELECT 1 FROM DUAL
       testWhileIdle: true
       testOnBorrow: false
       testOnReturn: false
       # 打开PSCache，指定每个连接上PSCache的大小
       poolPreparedStatements: true
       maxPoolPreparedStatementPerConnectionSize: 20
       # 配置监控统计拦截的filters，去掉后监控界面sql将无法统计，'wall'用于防火墙
       filters: stat, wall ,log4j
       # 通过connectProperties属性来打开mergeSql功能，慢SQL记录
       connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=5000
   ```

   设置type属性为`DruidDataSource`，可以配置Druid相关参数，打开监控

   ***此时，Druid数据源已经生效了***

3. 配置`statViewServlet`监控Servlet：

   创建一个配置类起名`DruidConfig`（类名随意）：

   ```java
   package com.example.config;
   
   import com.alibaba.druid.pool.DruidDataSource;
   import com.alibaba.druid.support.http.StatViewServlet;
   import com.alibaba.druid.support.http.WebStatFilter;
   import org.springframework.boot.context.properties.ConfigurationProperties;
   import org.springframework.boot.web.servlet.FilterRegistrationBean;
   import org.springframework.boot.web.servlet.ServletRegistrationBean;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   
   import javax.sql.DataSource;
   import java.util.HashMap;
   import java.util.Map;
   
   @Configuration
   public class DruidConfig {
   
       /**
        * 加载数据源到容器，引入配置文件中的配置
        * @return
        */
       @ConfigurationProperties(prefix = "spring.datasource")
       @Bean
       public DataSource druidDataSource(){
           return new DruidDataSource();
       }
   
       /**
        * 配置StatViewServlet
        * @return
        */
       @Bean
       public ServletRegistrationBean statViewServlet(){
           ServletRegistrationBean<StatViewServlet> bean = new ServletRegistrationBean<>(new StatViewServlet(), "/druid/*");
           //配置配置StatViewServlet的初始化参数
           HashMap<String, String> initParameters = new HashMap<>(10);
           //登陆的用户名密码
           initParameters.put("loginUsername","admin");
           initParameters.put("loginPassword","123");
           //允许谁可以访问(白名单)
           initParameters.put("allow","127.0.0.1");
           //禁止谁访问(黑名单)
           initParameters.put("liyan","192.168.1.123");
           //将存储初始化参数的map添加进来
           bean.setInitParameters(initParameters);
           return bean;
       }
   
       @Bean
       public FilterRegistrationBean webStatFilter(){
           //WebStatFilter过滤器（可以通过带参构造传入WebStatFilter实例，也可以通过set方法）
           FilterRegistrationBean bean = new FilterRegistrationBean(new WebStatFilter());
           //设置初始化参数
           Map<String,String> initParameters = new HashMap<>(10);
           initParameters.put("exclusions","*.js,/druid/*");
           bean.setInitParameters(initParameters);
           return bean;
       }
   }
   ```

   这里要了解两个类：

   - ServletRegistrationBean
   - FilterRegistrationBean

   在SpringBoot中，Servlet被内部集成，不需要配置`web.xml`，所以配置Servlet和Filter需要通过这两个类。

4. 访问监控页面：

   ```
   访问路径在配置Servlet时设置的
   localhost:8080/druid
   ```

   

### Druid Spring Boot Starter

Druid Spring Boot Starter 用于帮助你在Spring Boot项目中轻松集成Druid数据库连接池和监控。

[Github地址](https://github.com/alibaba/druid/tree/master/druid-spring-boot-starter)

Maven坐标：

```xml
<dependency>
  <groupId>com.alibaba</groupId>
  <artifactId>druid-spring-boot-starter</artifactId>
  <version>1.1.23</version>
</dependency>
```

配置文件：

```yaml
spring:
  profiles: dev
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/GATS_DB
      username: root
      password: 12345678
      # 初始化大小，最小，最大
      initial-size: 5
      min-idle: 5
      max-active: 20
      # 配置获取连接等待超时的时间(毫秒)
      max-wait: 3000
      # 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒
      time-between-eviction-runs-millis: 60000
      # 配置有一个连接在连接池中的最小生存时间，单位是毫秒
      min-evictable-idle-time-millis: 30000
      validation-query: SELECT 1 FROM DUAL
      test-while-idle: true
      test-on-borrow: false
      test-on-return: false
      # 打开PSCache，指定每个连接上PSCache的大小
      pool-prepared-statements: true
      max-pool-prepared-statement-per-connection-size: 20
      # 配置监控统计拦截的filters，去掉后监控界面sql将无法统计，'wall'用于防火墙
      filters: stat,wall
      # 通过connectProperties属性来打开mergeSql功能，慢SQL记录
      connection-properties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=5000
    type: com.alibaba.druid.pool.DruidDataSource
```

