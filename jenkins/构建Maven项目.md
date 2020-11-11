# 构建Maven项目

### Jenkins构建的项目类型介绍

Jenkins中自动构建项目的类型有很多，常用的有以下三种：

- 自由风格软件项目 (FreeStyle Project)
- Maven项目(Maven Project)
- 流水线项目 (Pipeline Project)

每种类型的构建其实都可以完成一样的构建过程和结果，只是在操作方式、灵活度等方面有所区别，在实际开发中可以根据自己的需求和习惯来选择。



### Maven项目构建

安装`Maven Integration plugin`插件。

新建任务，选择构建一个maven项目。它与自由风格项目不同点在于它就是通过maven构建项目：

![image-20201101210225380](https://images.shiguangping.com//imgs/20201101210225.png)
