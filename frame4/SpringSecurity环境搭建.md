# 5.24 SpringSecurity环境搭建

用到的页面素材已上传至码云：https://gitee.com/ENNRIAAA/spring-security-material



1. 创建SpringBoot项目，添加依赖：

   ```xml
   <!-- thymeleaf -->
   <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-thymeleaf</artifactId>
   </dependency>
   <!-- web -->
   <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

2. 将页面素材中static/qinjiang目录赋值到项目的static中，将素材中templates/index.html和views目录复制到项目的templates下：

   <img src="https://images.shiguangping.com/imgs/20200721191458.png" alt="image-20200721191458541" width="550px" />

3. 创建controller包，并创建`RouterController`：

   `resources/template`下的资源是不能直接被访问的，通过控制器路由各个页面。

   ```java
   @Controller
   public class RouterController {
   
       /**
        * 首页
        * @return
        */
       @RequestMapping({"/","/index"})
       public String index(){
           return "index";
       }
   
       /**
        * 登录页
        * @return
        */
       @RequestMapping("/toLogin")
       public String toLogin(){
           return "views/login";
       }
   
       /**
        * level1下的页面
        * @param id
        * @return
        */
       @RequestMapping("/level1/{id}")
       public String level1(@PathVariable("id") int id){
           return "views/level1/"+id;
       }
       /**
        * level2下的页面
        * @param id
        * @return
        */
       @RequestMapping("/level2/{id}")
       public String level2(@PathVariable("id") int id){
           return "views/level2/"+id;
       }
       /**
        * level3下的页面
        * @param id
        * @return
        */
       @RequestMapping("/level3/{id}")
       public String level3(@PathVariable("id") int id){
           return "views/level3/"+id;
       }
   }
   ```

   

