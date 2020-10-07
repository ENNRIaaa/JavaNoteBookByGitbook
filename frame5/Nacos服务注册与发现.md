# Nacos

## 服务提供者与消费者

服务提供者：服务的被调用方（即：为其他微服务提供接口的微服务）

服务消费者：服务的调用方（即：调用其他微服务接口的微服务）

*服务提供者将微服务注册到服务注册中心，服务消费者通过服务注册中心获取到服务接口并调用，如果服务提供者的信息发生改变，改变后的信息也会更新到注册中心，服务消费者依然可以正常调用该服务。*

## 大话剖析服务发现原理

![image-20200820004832351](https://images.shiguangping.com/imgs/20200829223430.png)

`last-heartbeat`心跳，微服务会定期向服务发现组件发送心跳，如果长时间没有发送心跳，则判定该服务当前状态不可用。

---

## Nacos

Nacos是Alibaba提供的服务注册与发现解决方案，官方文档：[https://nacos.io/zh-cn/index.html](https://nacos.io/zh-cn/index.html)

Nacos是既是服务发现组件，也是微服务的配置中心，可以管理微服务的所有配置。



引进Nacos组件后：

![image-20200820213740877](https://images.shiguangping.com/imgs/20200820213741.png)



下载并安装Nacos：[https://github.com/alibaba/nacos/releases](https://github.com/alibaba/nacos/releases)

在官方仓库下载nacos程序，根据官方文档快速开始安装运行Nacos。

## 注册应用到Nacos

**添加依赖：**

```xml
<dependency>
  <groupId>com.alibaba.cloud</groupId>
  <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

扩展：Spring Cloud Starter命名规律：

```xml
<dependency>
  <groupId>com.alibaba.cloud</groupId>
  <!--
        官方starter：spring-boot-starter-xxx
        非官方starter：xxx-spring-boot-starter
        spring-cloud-starter-{spring cloud子项目名称}-{模块名称}
-->
  <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

**添加注解：**

之前的版本需要在启动类中添加`@EnableDiscoveryClient`注解，现在可以不添加。

**写配置文件：**

```yaml
cloud:
    nacos:
      # 服务发现
      discovery:
        server-addr: localhost:8848
        
  application:
    # 服务名称，名称尽量使用'-'，不要用下划线或其他特殊字符
    name: user-center
```

`server-addr`是Nacos的服务器地址

`application.name`是服务名称

这些配置好之后启动应用，访问Nacos管理页面`localhost:8848/nacos`，在左侧服务列表中即可看到刚刚注册的服务。

![image-20200820215711884](https://images.shiguangping.com/imgs/20200829224107.png)

---

## Nacos服务发现的领域模型及元数据

![image-20200820221432780](https://images.shiguangping.com/imgs/20200829224217.png)

首先要记住，无法跨`Namespace`访问，即服务提供者和服务消费者处于不同的Namespace，则两者之间无法访问。