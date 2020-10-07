# 3.11 完整搭建一个SSM小项目√

```
Demo简介：数据库创建一个user表用来存储（id,username,password）,通过前端页面对数据库实现增删改查

用到的技术栈:
使用maven构建项目
开发工具：JetBranins IDEA 2020.01
后端：springMVC + spring + mybatis（数据库mysql，连接池druid）
前端：vue-cli + elementUI 异步通信axios
```



#### 准备工作：

1. 创建数据表（三个字段，id、username、password）

   <img src="https://images.shiguangping.com/imgs/20200626162648.png" alt="image-20200626162648849" width="500px" />

2. 使用IDEA创建一个普通的maven项目

   <img src="https://images.shiguangping.com/imgs/20200626162903.png" alt="image-20200626162903961" width="500px" />

3. 添加相关依赖

   不会Maven的话，可参见https://javabook.shiguangping.com/midd1/Maven.html 安装Maven、创建Maven项目

4. 项目工程结构：

   <img src="https://images.shiguangping.com/imgs/20200626213105.png" alt="image-20200626213105808" style="zoom:50%;" />

5. 下面开始从后端开始搭建这个项目



*项目功能比较简单，主要目的就是为了梳理、熟练SSM的搭建思路和流程*



搭建顺序从后端到前端，依次是：

1. Mybatis部分
2. Spring部分
3. SpringMVC部分
4. 使用vue脚手架创建项目，实现增删改查，异步通信使用的是axios库



先把实体类创建上：

```java
package com.neu.pojo;

/**
 * 实体类User
 */
public class User {
    /**
     * 属性名尽量与数据库表的字段名相同
     */
    private int id;
    private String username;
    private String password;

    /**
     * 构造方法和getter/setter方法、toString方法都要写
     * Spring的DI（依赖注入）主要是通过setter方法进行注入的，所有Set方法是必须的
     */
    public User() {
    }

    public User(int id, String username, String password) {
        this.id = id;
        this.username = username;
        this.password = password;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}
```

