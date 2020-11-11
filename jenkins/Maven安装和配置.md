# Maven 安装和配置

在`/opt`目录下新建并切换到`maven`目录：

```bash
mkdir maven && cd maven
```

下载maven压缩包到当前目录：

```bash
wget https://apachemirror.sg.wuchna.com/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
```

解压并切换到解压后的maven目录：

```bash
tar -zxvf apache-maven-3.6.3-bin.tar.gz
cd apache-maven-3.6.3
```

配置环境变量：

```bash
vim /etc/profile
```

在配置文件最后添加：

![image-20201101170433035](https://images.shiguangping.com//imgs/20201101170433.png)

使配置文件生效：

```bash
source /etc/profile
```

查看maven是否配置成功：

```bash
mvn -version
```

![image-20201101170607777](https://images.shiguangping.com//imgs/20201101170607.png)

修改maven仓库路径和配置阿里云镜像源：

在maven根目录下新建`repo`目录用于存放下载的依赖，再切换到maven的conf目录下修改配置文件：

```bash
vim setting.xml
```

将本地仓库地址改为刚刚新建的`repo`路径：

![image-20201101171645525](https://images.shiguangping.com//imgs/20201101171645.png)

配置阿里云镜像源：

```xml
<mirrors>
  <mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>        
  </mirror>
</mirrors>
```

![image-20201101171939330](https://images.shiguangping.com//imgs/20201101171939.png)

Jenkins系统管理 -> 全局工具配置中添加jdk和maven：

![image-20201101172205733](https://images.shiguangping.com//imgs/20201101172205.png)

![image-20201101172222698](https://images.shiguangping.com//imgs/20201101172222.png)

在系统管理 -> 系统配置中添加全局属性：

![image-20201101172324208](https://images.shiguangping.com//imgs/20201101172324.png)



>FAQ:
>
>本地环境搭建的Jenkins，使用上述方式在本地安装maven。使用Docker部署的Jenkins，需要在Docker容器内安装maven、jdk等。



回到Jenkins首页，选择之前拉取代码的任务，在配置中添加构建脚本，拉取代码后执行打包操作：

![image-20201101195944786](https://images.shiguangping.com//imgs/20201101195949.png)

配置完后，立即构建：

![image-20201101200323301](https://images.shiguangping.com//imgs/20201101200323.png)