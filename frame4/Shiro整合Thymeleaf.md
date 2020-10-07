# 5.35 Shiro整合Thymeleaf

1. 导入thymeleaf-shiro整合包：

   ```xml
   <dependency>
     <groupId>com.github.theborakompanioni</groupId>
     <artifactId>thymeleaf-extras-shiro</artifactId>
     <version>2.0.0</version>
   </dependency>
   ```

2. `index.html`添加shiro命名空间：

   ```html
   <html lang="en" xmlns:th="http://www.thymeleaf.org"
         xmlns:shiro="http://www.pollix.at/thymeleaf/shiro">
   ```

3. 在thymeleaf页面添加shiro属性：

   ![image-20200725231052947](https://images.shiguangping.com/imgs/20200725231053.png)



***到此为止，整合Shiro结束，案例源码已上传至码云https://gitee.com/ENNRIAAA/springboot-shiro-learning***

