# 1.2 配置环境变量

JDK安装完成之后，就需要给系统配置Java环境变量了。  

**配置环境变量：桌面计算机右键属性-->高级系统设置-->环境变量**

<img src="https://images.shiguangping.com/images/Java%E5%AD%A6%E4%B9%A0%E4%B9%8B_%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E5%AE%89%E8%A3%85/Java%E5%AD%A6%E4%B9%A0%E4%B9%8B_%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E5%AE%89%E8%A3%85_%E5%9B%BE2.png" width="400px"/>

在**系统变量**中`新建`变量`JAVA_HOME`(如上图)：

- 变量名：JAVA_HOME

- 变量值：JDK的安装路径



*JDK的默认安装路径一般在C盘下Program Files -->Java文件夹下，参考下图。*

*（路径一定要全，复制到jdk文件夹下的bin文件夹）*

<img src="https://images.shiguangping.com/images/Java%E5%AD%A6%E4%B9%A0%E4%B9%8B_%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E5%AE%89%E8%A3%85/Java%E5%AD%A6%E4%B9%A0%E4%B9%8B_%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E5%AE%89%E8%A3%85_%E5%9B%BE3.png" width="450px"/>

`编辑`系统变量中的`Path`，在`path`的值中加入一条 `%JAVA_HOME%\bin;`



### 验证是否安装成功

环境变量配置好后，在cmd窗口敲入命令：

```shell
java -version
```

<img src="https://images.shiguangping.com/images/Java%E5%AD%A6%E4%B9%A0%E4%B9%8B_%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E5%AE%89%E8%A3%85/Java%E5%AD%A6%E4%B9%A0%E4%B9%8B_%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E5%AE%89%E8%A3%85_%E5%9B%BE5.png" width="400px"/>

终端提示Java版本号，说明环境变量配置成功。

*如果没有配置成功，终端会显示【不是内部或外部命令，也不是可运行的程序或批处理文件】。* 