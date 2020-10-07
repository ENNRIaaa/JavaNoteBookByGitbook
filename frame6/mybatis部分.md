# 4.1 Mybatis部分（持久层）

使用SSM框架搭建项目，离不开各种各样的配置文件，因此，

第一步，先在resources中创建Mybatis的核心配置文件文件，`mybatis-config.xml`，

再创建一个`database.properties`用来配置数据库的相关信息：

#### database.properties：

<img src="https://images.shiguangping.com/imgs/20200626221953.png" alt="image-20200626221953925" width="700px" />

#### mybatis-config.xml：

之后会通过Spring来整合Mybatis，所以在Mybatis的配置文件中，我只配置了实体类的别名，和注册Mapper。

配置数据源的工作，交给了Spring去做，之后会在Spring的配置文件中配置。

<img src="https://images.shiguangping.com/imgs/20200626223649.png" alt="image-20200626223649794" width="700px" />



### 编写Dao层：

#### UserMapper接口

<img src="https://images.shiguangping.com/imgs/20200626224222.png" alt="image-20200626224222566" width="700px" />



#### UserMapper.xml

相当于之前的UserDaoImpl实现类，SQL语句就在这里写：

![image-20200626224545708](https://images.shiguangping.com/imgs/20200626224545.png)



### 编写Service层：

#### UserService.java接口

![image-20200626225448770](https://images.shiguangping.com/imgs/20200626225448.png)

#### UserServiceImpl.java实现类

<img src="https://images.shiguangping.com/imgs/20200626225628.png" alt="image-20200626225628068" width="700px" />

UserServiceImpl中会生命一个Dao层接口的对象，用来调用Dao层方法操作数据库，这里要记得添加setter方法，完成依赖注入。否则，会报错。

*（没有使用注解，完全通过配置文件注册Bean）*

****

***到这里，Mybatis相关的就写完了，接下来开始配置Spring***

