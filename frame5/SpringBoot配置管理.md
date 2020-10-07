# Spring Boot配置管理

## 支持的配置格式

Spring Boot除了`application.properties`之外，

还支持`application.yaml`或者`applicaiton.yml`



yaml：Yet Anther Markup Language（还有另一种标记语言） ==> Json的子集



## Spring Boot配置管理的17种姿势

1. [Devtools global settings properties](https://docs.spring.io/spring-boot/docs/2.1.9.RELEASE/reference/html/using-boot-devtools.html#using-boot-devtools-globalsettings) on your home directory (`~/.spring-boot-devtools.properties` when devtools is active).
2. [`@TestPropertySource`](https://docs.spring.io/spring/docs/5.1.10.RELEASE/javadoc-api/org/springframework/test/context/TestPropertySource.html) annotations on your tests.
3. `properties` attribute on your tests. Available on [`@SpringBootTest`](https://docs.spring.io/spring-boot/docs/2.1.9.RELEASE/api/org/springframework/boot/test/context/SpringBootTest.html) and the [test annotations for testing a particular slice of your application](https://docs.spring.io/spring-boot/docs/2.1.9.RELEASE/reference/html/boot-features-testing.html#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests).
4. Command line arguments.
5. Properties from `SPRING_APPLICATION_JSON` (inline JSON embedded in an environment variable or system property).
6. `ServletConfig` init parameters.
7. `ServletContext` init parameters.
8. JNDI attributes from `java:comp/env`.
9. Java System properties (`System.getProperties()`).
10. OS environment variables.
11. A `RandomValuePropertySource` that has properties only in `random.*`.
12. [Profile-specific application properties](https://docs.spring.io/spring-boot/docs/2.1.9.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties) outside of your packaged jar (`application-{profile}.properties` and YAML variants).
13. [Profile-specific application properties](https://docs.spring.io/spring-boot/docs/2.1.9.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties) packaged inside your jar (`application-{profile}.properties` and YAML variants).
14. Application properties outside of your packaged jar (`application.properties` and YAML variants).
15. Application properties packaged inside your jar (`application.properties` and YAML variants).
16. [`@PropertySource`](https://docs.spring.io/spring/docs/5.1.10.RELEASE/javadoc-api/org/springframework/context/annotation/PropertySource.html) annotations on your `@Configuration` classes.
17. Default properties (specified by setting `SpringApplication.setDefaultProperties`).



## 配置管理常用方式

- 配置文件 --- yaml、properties

- 环境变量

  ```yaml
  management:
    endpoint:
      health:
        show-details: ${SOME_ENV}
  ```

  `show-details`读取环境变量，并在运行配置中设置环境变量：

  <img src="https://images.shiguangping.com/imgs/20200817220256.png" alt="image-20200817220256232" width="500px" />

  #### 可执行Jar：

  使用`mvn clean install`重新构建项目，此时会报错，因为运行这个命令会执行单元测试，单元测试中的启动类会读取配置文件，配置文件中涉及环境变量。由于环境变量是配置在IDEA中，所以在命令行中读取不到。

  这是可以把测试类干掉，或者跳过单元测试：

  ```
  mvn clean install -DskipTests
  ```

  构建好Jar包之后，执行Jar包：(同样也需要声明环境变量)

  ```
  java -jar spring-boot-demo-0.0.1-SNAPSHOT.jar --SOME_ENV=always
  ```

- 外部配置文件

  <img src="https://images.shiguangping.com/imgs/20200817221829.png" alt="image-20200817221829544" width="500px" />

  将可执行Jar包和yml配置文件放到同一个文件夹，并将`always`改为`never`,再执行Jar包：

  <img src="https://images.shiguangping.com/imgs/20200817222001.png" alt="image-20200817222001807" width="500px" />

  说明Jar包运行时可以读取同一目录中配置文件，说明Jar包**外面的配置文件比Jar内置的配置文件优先级更高**。

- 命令行参数

  在运行/调试配置中，设置程序参数：

  <img src="https://images.shiguangping.com/imgs/20200817222259.png" alt="image-20200817222259019" width="500px" />

  如果是执行可执行Jar包：

  ```
  java -jar spring-boot-demo-0.0.1-SNAPSHOT.jar --server.port=8082
  ```

  

## 最佳实践

简单即是美，尽量规避优先级问题

