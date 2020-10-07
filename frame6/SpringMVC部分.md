# 4.3 SpringMVC部分

#### 1.添加web框架支持

首先，项目添加web框架支持，配置web.xml（如果一开始创建的是Web项目，则忽略这一步）

<img src="https://images.shiguangping.com/imgs/20200626235105.png" alt="image-20200626235105665" width="700px" />

紧接着，要把各种依赖添加到Tomcat中：

![image-20200627150140702](https://images.shiguangping.com/imgs/20200627150140.png)

Tomcat在运行时，会调用WEB-INF/lib中的依赖



#### 2. 配置web.xml

![image-20200627000943707](https://images.shiguangping.com/imgs/20200627000943.png)

SpringMVC的核心就是DispatcherServlet，一切都是围绕这它展开的。

*`DispatcherServlet`是一个核心分发器，所有的请求都会经过它，再由它去分发给能处理该请求的控制器，它是SpringMVC的核心所在。*

在web.xml中也可以配置过滤器，来解决像中文乱码等问题。



#### 3. spring-mvc.xml

配置SpringMVC的配置文件，如果需要返回指定视图，则需要配置视图解析器

![image-20200627001727990](https://images.shiguangping.com/imgs/20200627001728.png)

*如果配置了第三步组件扫描包，可以省略第一步开启注解驱动*



#### 4.编写Controller控制器

在pojo包下创建一个实体类`RespMsg`，用来封装响应给前端的信息：

<img src="https://images.shiguangping.com/imgs/20200627152153.png" alt="image-20200627152153218" width="600px" />



#### 控制类：

- 在SpringMVC中，被`@Controller`注解的类会被注解为控制类，并在容器中自动注册Bean

- 控制类中常用的注解：

  - `@Controller`：控制类

  - `@RequestMapping`请求映射，可以作用在类上或方法上

  - 衍生注解：`@GetMapping`：get请求、`@PostMapping`：post请求

  - `@CrossOrigin`：跨域请求

    

和Servlet不同的是，Servlet每实现一个功能就要写一个Servlet类；而SpringMVC中只需要在一个控制类中编写多个方法就可以实现不同的功能，使用注解为每个方法设置url-pattern。



**编写控制类中的方法：**

![image-20200627151918025](https://images.shiguangping.com/imgs/20200627151918.png)

*每个方法都添加了`@ResponseBody`注解，用来响应给前端字符串。也可以使用`@RestController`来替换`@Controller`，省略方法的`@ResponseBody`注解，实现相同的功能。*



#### 配置Tomcat，运行后端程序

![image-20200627153248836](https://images.shiguangping.com/imgs/20200627153248.png)

这块就不多说了，直接测试：

- 添加User：

  ![image-20200627153527345](https://images.shiguangping.com/imgs/20200627153527.png)

- 查询全部User：

  ![image-20200627153600328](https://images.shiguangping.com/imgs/20200627153600.png)

  这里发现显示中文有乱码：添加一个过滤器试试





***后端部分到这儿结束，接下来开始创建前端项目***