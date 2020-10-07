# IDEA创建SpringBoot程序

通过IDEA快速构建项目：（IDEA也是通过Spring官网构建的项目）

![image-20200627204904093](https://images.shiguangping.com/imgs/20200627215751.png)

下一步：

![image-20200627220019766](https://images.shiguangping.com/imgs/20200627220019.png)

下一步，可以添加依赖，然后选择项目路径，创建完毕。



如果创建时没有添加Web依赖，创建完毕后，可以在pom文件种添加：

![image-20200627220208908](https://images.shiguangping.com/imgs/20200627220208.png)

写一个Controller：

![image-20200627220556725](https://images.shiguangping.com/imgs/20200627220556.png)

浏览器访问：

![image-20200627220622309](https://images.shiguangping.com/imgs/20200627220622.png)

*访问正常*



**如何修改Tomcat端口号？**

- 在`application.properties`中设置端口号：

  ```properties
  # 修改Tomcat端口号
  server.port=8081
  ```

- 通过IDEA设置：

  ![image-20200627220823415](https://images.shiguangping.com/imgs/20200627220823.png)



**彩蛋：如何修改banner？**

什么是banner？答：SpringBoot运行起来时的横幅：

![image-20200627221019288](https://images.shiguangping.com/imgs/20200627221019.png)

Google搜索“Spring Boot banner生成”，有很多这样的网站，例如：https://www.bootschool.net/ascii

在`resources`下新建一个`banner.txt`文件，注意名字不要错，把生成好的banner文本粘贴到txt文件中保存

![image-20200627221407122](https://images.shiguangping.com/imgs/20200627221407.png)

重启Spring Boot：

![image-20200627221434244](https://images.shiguangping.com/imgs/20200627221434.png)

