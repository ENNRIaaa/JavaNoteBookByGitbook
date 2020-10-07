# 5.34 Shiro请求授权实现

1. Shiro过滤器添加访问过滤：

   ```java
   // 拥有perms[user]权限可以访问
   filterMap.put("/user/add","perms[user:add]");
   filterMap.put("/user/update","perms[user:update]");
   
   // 设置未经授权url
   bean.setUnauthorizedUrl("/unauthorized");
   ```

   有指定许可的用户才可以访问指定功能

2. 数据库表添加`perms`字段：

   <img src="https://images.shiguangping.com/imgs/20200725121142.png" alt="image-20200725121142347" style="zoom:50%;" />

3. 在`UserRealm`中设置许可：

   ![image-20200725121519820](https://images.shiguangping.com/imgs/20200725121519.png)





***到此处，登陆admin1，可以访问add页面，不能访问update；登陆admin2可以访问update，不能访问add***