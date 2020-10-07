# 4.2 Spring部分

*Spring是一个容器，它就像是一个大管家一样，管理着项目上所有的对象*

Spring的核心思想之一：就是控制反转(IoC)，

- 之前，都是我们手动去new对象，对象间的关系完全是由我们程序猿来控制；
- 现在，所有的对象都交由Spring的IoC容器去管理，对象间的关系也由Spring自动去注入，把控制权交由Spring，这就是控制反转的思想。

---

*使用Spring一开始，依旧是创建配置文件，通过配置文件完成Bean的注册*



#### 创建ApplicationContext.xml

先在resources下创建一个总的Spring配置文件，再分别创建不同的配置文件来配置Dao层、Service层和Controller层，

最后再把这三个配置文件通过`import`标签导入到`ApplicationContext.xml`中

*（也可以把所有的配置写在一个xml文件里，但如果对对象之间的关系不是很清晰的话，分开写比较容易理清它们之间的关系）*

![image-20200626235731643](https://images.shiguangping.com/imgs/20200626235731.png)



#### 2. spring-dao.xml 整合Dao层：

![image-20200626233112402](https://images.shiguangping.com/imgs/20200626233112.png)

这一步做了什么？

- 引入数据库配置文件`database.properties`
- 创建数据源`dataSource`，这里使用的是Alibaba的Druid，所以class=`DruidDataSource`
  - 这里可以使用任意的数据源，例如Spring的数据源、C3P0等
- 注册SqlSessionFactory
  - 这个是Mybatis-Spring中非常核心的对象，有了它，就可以完成Mybatis的所有操作。具体可参见我的[Spring整合Mybatis的笔记]([https://javabook.shiguangping.com/frame1/%E6%95%B4%E5%90%88Mybatis.html](https://javabook.shiguangping.com/frame1/整合Mybatis.html))
- 配置Mapper扫描，自动将Mapper注册到Spring容器中
  - 这一步是通过扫描`com.neu.dao`包，自动将映射器注册到Spring容器中，不需要我们手动去配置每一个映射器(Mapper)



#### 3. spring-service.xml 整合service层：

![image-20200626234527033](https://images.shiguangping.com/imgs/20200626234527.png)

这一步做了什么？

- 1. 组件扫描，扫描指定包下的注解，如`@Component`、`@Service`、`@Repository`、`@Controller`，将被注解的类自动注册Bean
- 2. 不使用注解的话，可以手动在Spring中注册Bean，完成依赖注入

*（如果不使用注解的话，可以不写第一步；如果使用注解自动注册、自动装配的话，可以不写第二步）*



#### 4. 将配置文件引入到ApplicationContext.xml中

将`spring-dao.xml`和`spring-service.xml`引入到`ApplicationContext.xml`中：

![image-20200626235857742](https://images.shiguangping.com/imgs/20200626235857.png)





***Spring整合mybatis部分到这儿就结束了，接下来开始配置SpringMVC***

