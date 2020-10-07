# 3.2 SpringMVC使用注解开发

### 代码示例：

1. 配置web.xml（使用version 4.0）

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
     <!--注册DispatcherServlet-->
     <servlet>
       <servlet-name>springmvc</servlet-name>
       <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
       <!--关联SpringMVC配置文件-->
       <init-param>
         <param-name>contextConfigLocation</param-name>
         <param-value>classpath:springmvc-servlet.xml</param-value>
       </init-param>
       <load-on-startup>1</load-on-startup>
     </servlet>
     <!--映射路径，/表示出了jsp请求外的所有请求都会被DispatcherServlet拦截-->
     <servlet-mapping>
       <servlet-name>springmvc</servlet-name>
       <url-pattern>/</url-pattern>
     </servlet-mapping>
   </web-app>
   ```

2. 配置springmvc-servlet.xml：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xmlns:mvc="http://www.springframework.org/schema/mvc"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">
   
     <!--自动扫描包，让指定包下的注解生效，由IoC容器统一管理-->
     <context:component-scan base-package="com.neu.controller"/>
   
     <!--让springmvc不处理静态资源-->
     <mvc:default-servlet-handler/>
   
     <!--支持mvc注解驱动
               在spring中一般采用@RequestMapping注解来完成映射关系
               要想使@RequestMapping注解生效
               必须向上下文中注册DefaultAnnotationHandlerMapping
               和AnnotationMethodHandlerAdapter实例
               这两个实例分别在类级别和方法级别处理。
               而annotation-driven配置帮助我们自动完成上述两个实例的注入。-->
     <mvc:annotation-driven/>
   
     <!--视图解析器-->
     <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
       <property name="prefix" value="/WEB-INF/jsp/"/>
       <property name="suffix" value=".jsp"/>
     </bean>
   </beans>
   ```

3. 编写Controller类：

   ```java
   package com.neu.controller;
   
   import org.springframework.stereotype.Controller;
   import org.springframework.ui.Model;
   import org.springframework.web.bind.annotation.RequestMapping;
   
   @Controller
   @RequestMapping("demo")
   public class HelloController {
       @RequestMapping("/hello")
       public String hello(Model model) {
           //封装数据
           model.addAttribute("msg", "Hello SpringMVC!");
           //返回的字符串会被视图解析器处理
           return "hello";
       }
   }
   ```

   这里面需要解释一下：

   - `@Controller`注解，（省去了之前需要实现Controller接口的步骤）

   - `@RequestMapping("/hello")`注解，（省去了在配置文件中配置Handler映射和配置Handler）；

     该注解既可以作用于类，也可以作用于方法，像案例中类和方法中都使用了注解，则访问地址为`http://localhost:8080/springmvc_03_annotation/demo/hello`，要注意访问路径的层级关系。

   - 之前的Servlet实现一个功能就要写一个Servlet类，而现在只需要定义方法即可，使用`@RequestMapping()`注解

   - 方法return的字符串返回的是ViewName，该字符串会传递给视图解析器，通过解析器得到完整的视图资源路径，最后交由DispatcherServlet，给用户响应最终的视图资源。



***如果需要返回像Json字符串，可以通过`@RestController`注解，该注解下返回的字符串不会被视图解析器解析，而是直接返回字符串***

#### 最后小结：

SpringMVC使用注开发步骤：

1. 新建一个Web项目
2. 导入相关依赖
3. 编写web.xml，注册DispatcherServlet
4. 编写SpringMVC配置文件
5. 创建对应的控制类，Controller
6. 完善前端视图和Controller之间的对应关系
7. 测试运行调试



使用SpringMVC必须配置的三大件：

- 处理器映射器
- 处理器适配器
- 视图解析器

通常我们只需要手动配置视图解析器即可，而处理器映射器和处理器适配器只需要开启注解驱动即可