# Eclipse配置Maven

1. 进入Eclipse -> Window -> Preferences：

   ![image-20200626195038646](https://images.shiguangping.com/imgs/20200626195038.png)

   添加maven路径：

   ![image-20200626195056549](https://images.shiguangping.com/imgs/20200626195056.png)

   选中刚刚添加进来的maven:

   ![image-20200626195111793](https://images.shiguangping.com/imgs/20200626195111.png)

2. 设置User Setting：

   ![image-20200626195124932](https://images.shiguangping.com/imgs/20200626195124.png)

   在Global Setting中添加maven的配置文件，添加进来之后，会看到Local Repository自动更新成了在`setting.xml`中配置的repo的路径。

   User Setting也添加一下maven的配置文件，最后看到的设置页面就是这个样子：

   ![image-20200626195135163](https://images.shiguangping.com/imgs/20200626195135.png)



**到这里，Eclipse的maven就配置完成了，下面我们来创建一个普通的maven项目**



### 使用Eclipse创建一个普通的Maven项目

1. 打开Eclipse -> File -> New -> Maven Project：

   ![image-20200626195211156](https://images.shiguangping.com/imgs/20200626195211.png)

   下一步：

   ![image-20200626195310703](https://images.shiguangping.com/imgs/20200626195310.png)

2. 点击Finish，项目创建完成：

   ![image-20200626195323672](https://images.shiguangping.com/imgs/20200626195323.png)

3. 测试一下Jdbc：

   ![image-20200626195338398](https://images.shiguangping.com/imgs/20200626195338.png)





总结：

- 安装maven前要安装好jdk环境
- maven不要安装在系统目录下或者要求管理员权限访问的目录（会出现maven没有权限访问的问题）
- 本地仓库的路径设置不是必要的，这个因人而异