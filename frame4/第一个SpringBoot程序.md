# 第一个SpringBoot程序

通过Spring官网快速构建项目：https://start.spring.io/：

![image-20200627210633360](https://images.shiguangping.com/imgs/20200627210633.png)

点击生成之后，会自动下载生成的项目，以zip压缩包的形式，然后解压到本地，再通过IDEA导入项目：

![image-20200627211639821](https://images.shiguangping.com/imgs/20200627211639.png)

写一个Controller测试一下：

![image-20200627212536467](https://images.shiguangping.com/imgs/20200627212536.png)



---

通过Maven打一个Jar包跑一下：

![image-20200627212818329](https://images.shiguangping.com/imgs/20200627212818.png)

*如果打包失败，检查一下Maven的环境配置*

在终端通过`java -jar xxx.jar`命令运行刚刚打包好的jar包：

![image-20200627213114734](https://images.shiguangping.com/imgs/20200627213114.png)

在浏览器访问一下：

![image-20200627213359840](https://images.shiguangping.com/imgs/20200627213359.png)

*jar包就是一个可执行程序，由于默认内嵌了Tomcat，运行jar包，浏览器可以访问*

*测试结束后要`ctrl+c`结束程序，否则8080会一直被占用*

