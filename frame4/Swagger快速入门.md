# 5.36 Swagger快速入门

#### Quick Start

1. 搭建SpringBoot项目，创建`HelloController`：

   ```java
   @RestController
   public class HelloController {
   
       @RequestMapping("/hello")
       public String hello(){
           return "Hello SpringBoot";
       }
   }
   ```

2. 导入Swagger依赖：

   ```xml
   <!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger2 -->
   <dependency>
     <groupId>io.springfox</groupId>
     <artifactId>springfox-swagger2</artifactId>
     <version>2.9.2</version>
   </dependency>
   
   <!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui -->
   <dependency>
     <groupId>io.springfox</groupId>
     <artifactId>springfox-swagger-ui</artifactId>
     <version>2.9.2</version>
   </dependency>
   ```

3. 配置Swagger，创建`SwaggerConfig`：

   ```java
   @Configuration
   @EnableSwagger2
   public class SwaggerConfig {
   
   }
   ```

4. 访问Swagger的ui：

   ```
   http://localhost:8080/swagger-ui.html
   ```

   <img src="https://images.shiguangping.com/imgs/20200726003449.png" alt="image-20200726003449245" width="650px" />

5. 自定义ui页面的信息：

   ```java
   @Configuration
   @EnableSwagger2
   public class SwaggerConfig {
   
       /**
        * 加载Swagger Bean
        * Docket是Swagger的实例
        *
        * @return
        */
       @Bean
       public Docket docket() {
           return new Docket(DocumentationType.SWAGGER_2)
                   .apiInfo(apiInfo());
       }
   
       /**
        * 自定义Swagger ApiInfo
        * @return
        */
       private ApiInfo apiInfo() {
           // 联系方式
           Contact contact = new Contact("liyan","http://www.shiguangping.com","18525589998@163.com");
   
           return new ApiInfo("Api Documentation", "李炎学习Swagger", "1.0", "urn:tos",
                   contact, "Apache 2.0", "http://www.apache.org/licenses/LICENSE-2.0", new ArrayList<VendorExtension>());
       }
   }
   ```



#### 配置扫描接口：

```java
    @Bean
    public Docket docket() {
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo()).select()
                // RequestHandlerSelectors 配置请求处理选择器，用来配置选择哪些api
                .apis(RequestHandlerSelectors
                        // basePackage() 指定包下的接口都会被选择
                        // any() 所有接口都选择
                        // none() 所有接口都不选择
                        // withMethodAnnotation() 选择方法上的注解作用的接口，参数是注解的类对象
                        // withClassAnnotation() 选择类上的注解作用的接口，参数是注解的类对象
                        .basePackage("com.example.controller"))
                // PathSelectors 路径选择器，指定选择的接口路径
                .paths(PathSelectors.ant("/user/**"))
                .build();
    }
```

配置哪些接口会被Swagger扫描到：

RequestHandlerSelectors 配置请求处理器选择器（就是控制类中的方法），用来配置选择哪些api：

- basePackage() 指定包下的接口都会被选择

- any() 所有接口都选择

- none() 所有接口都不选择

- withClassAnnotation() 选择类上的注解作用的接口，参数是注解的类对象

- withMethodAnnotation() 选择方法上的注解作用的接口，参数是注解的类对象

PathSelectors可以指定接口路径选择接口：

- ant() 指定路径



#### 开启或关闭Swagger：

```java
@Bean
public Docket docket() {
  return new Docket(DocumentationType.SWAGGER_2)
    .apiInfo(apiInfo())
    // 关闭Swagger，浏览器无法访问Swagger-UI
    .enable(false)
    .select()
```

- enable(false) 关闭Swagger



#### 如何在开发环境中启用Swagger，在上线时停用Swagger？

**方式一：**

```java
@Bean
public Docket docket(Environment env) {
  // 匹配div配置文件创建Profiles实例
  Profiles profiles = Profiles.of("dev");
  // 判断当前激活的配置文件是否是指定配置文件，如果当前激活的是dev，则返回true
  boolean flag = env.acceptsProfiles(profiles);

  return new Docket(DocumentationType.SWAGGER_2)
    .apiInfo(apiInfo())
    // 关闭Swagger，浏览器无法访问Swagger-UI
    .enable(flag)
```



**方式二：**注解

在`application-dev.yml`（开发环境）中添加`swagger.show=true`的属性：

```yaml
swagger:
  show: true
```

然后，在Swagger配置类中自定义一个布尔类型参数并读取配置文件注入值：

```java
@Value("${swagger.show}")
private boolean swaggerShow;

return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .enable(swaggerShow)
```

把值传给`enable()`来停用或者启用Swagger。



#### Swagger分组：

```java
// 定义组名称
.groupName("liyan")
```

一个Docket实例是一个分组，定义多个Docket实例可以定义多个分组



Swagger注释相关的注解：

- `@ApiModel("User实体类")`：给实体类添加注释，作用在类上
- `@ApiModelProperty("用户id")`：给实体类参数添加注释
- `@ApiOperation("hello接口")`：给RequestHandler添加注释，控制类方法
- `@ApiParam("用户名")`：给RequestHandler参数添加注释

