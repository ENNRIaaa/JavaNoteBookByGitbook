# Maven

### 安装maven

1. 官方下载地址：http://maven.apache.org/

   ![image-20200626194629722](https://images.shiguangping.com/imgs/20200626194629.png)

2. 将压缩包解压到一个固定的位置

   ![image-20200626194643757](https://images.shiguangping.com/imgs/20200626194643.png)

   *放到一个固定的位置，maven的路径不能轻易改动，这个涉及到下一步要配置的环境变量*

3. 添加环境变量

   桌面右键“此电脑” -> 属性 -> 高级系统设置 -> 环境变量 ->系统变量：

   ![image-20200626194659747](https://images.shiguangping.com/imgs/20200626194659.png)

   编辑Path：

   ![image-20200626194711217](https://images.shiguangping.com/imgs/20200626194711.png)

   点击**确定**，把所有窗口关掉，关闭窗口都要点击确定来关闭，以免发生不测

4. 打开CMD窗口，输入命令：

   ```shell
   mvn -v
   ```

   ![image-20200626194732821](https://images.shiguangping.com/imgs/20200626194732.png)

   *显示Maven版本等信息，说明Maven安装成功，如果提示非内部或外部命令，则检查一下环境变量是否配置正确。*

5. 修改maven的配置文件：（路径：maven/conf/setting.xml）

   ![image-20200626194743054](https://images.shiguangping.com/imgs/20200626194743.png)

使用文本编辑工具打开`setting.xml`，没有文本编辑工具的推荐下载使用sublime，它是一个轻量级的文本编辑工具，比较好用

这里主要设置两个地方：

- repo仓库的存储路径

  这个本地仓库的作用是，我们在maven项目的pom.xml中添加依赖坐标之后，maven会先到这个本地仓库去找有没有这个依赖资源。如果有，就直接从本地仓库把依赖导入到项目中；如果没有就会到maven的中央仓库中下载，把依赖下载到本地仓库，然后再自动导入到项目中

- 修改下载源

步骤：

1. 在maven根目录新建一个文件夹repo（文件夹名称和路径自定义，这个文件夹是用来存放maven下载的各种依赖的仓库）

   ![image-20200626194756036](https://images.shiguangping.com/imgs/20200626194756.png)

   在`setting.xml`中设置本地仓库的路径

   ![image-20200626194806013](https://images.shiguangping.com/imgs/20200626194806.png)

2. 添加阿里镜像仓库

   ![image-20200626194815611](https://images.shiguangping.com/imgs/20200626194815.png)

   在mirrors标签中添加

   ```xml
   <mirror>
       <id>alimaven</id>
       <name>aliyun maven</name>
       <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
       <mirrorOf>central</mirrorOf>        
   </mirror>
   ```

   

**以上Maven的安装和配置就结束了。**

