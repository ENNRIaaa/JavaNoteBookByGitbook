# Spring Boot Actuator

### Actuator 监控

Spring Boot 使用“习惯优于配置的理念”，采用包扫描和自动化配置的机制来加载依赖 Jar 中的 Spring bean，不需要任何 Xml 配置，就可以实现 Spring 的所有配置。虽然这样做能让我们的代码变得非常简洁，但是整个应用的实例创建和依赖关系等信息都被离散到了各个配置类的注解上，这使得我们分析整个应用中资源和实例的各种关系变得非常的困难。

Actuator 是 Spring Boot 提供的对应用系统的自省和监控的集成功能，可以查看应用配置的详细信息，例如自动化配置信息、创建的 Spring beans 以及一些环境属性等。

为了保证 actuator 暴露的监控接口的安全性，需要添加安全控制的依赖`spring-boot-start-security`依赖，访问应用监控端点时，都需要输入验证信息。Security 依赖，可以选择不加，不进行安全管理，但不建议这么做。



## 1、添加依赖

```xml
<!-- actuator依赖 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```



## 2、启动应用

依赖添加好之后，启动应用：

浏览器访问：`http://localhost:8080/actuator`，会看到Actuator暴露的端点：

<img src="https://images.shiguangping.com/imgs/20200817212307.png" alt="image-20200817212307545" style="zoom:50%;" />



## 健康状态检查

浏览器访问：`http://localhost:8080/actuator/health`查看健康状态，在配置文件中配置显示健康详情：

```yaml
# 显示健康详情
management:
  endpoint:
    health:
      show-details: always
```

![image-20200817212628739](https://images.shiguangping.com/imgs/20200817212628.png)

`status`取值：

- UP：正常
- DOWN：遇到了问题，不正常
- OUT_OF_SERVICE：资源未在使用，或者不该去使用
- UNKNOW：不知道



## 设置应用描述

```yaml
# 用来描述应用
info:
  app-name: spring-boot-demo
  author: liyan
  mail: xxx@qq.com
```

`info`下key: value字段都是自定义的、

![image-20200817213340451](https://images.shiguangping.com/imgs/20200817213340.png)



## Actuator 提供了 13 个端点，具体如下表所示：

| HTTP 方法 | 路径            | 描述                                                         |
| :-------- | :-------------- | :----------------------------------------------------------- |
| GET       | /auditevents    | 显示应用暴露的审计事件 (比如认证进入、订单失败)              |
| GET       | /beans          | 描述应用程序上下文里全部的 Bean，以及它们的关系              |
| GET       | /conditions     | 就是 1.0 的 /autoconfig ，提供一份自动配置生效的条件情况，记录哪些自动配置条件通过了，哪些没通过 |
| GET       | /configprops    | 描述配置属性(包含默认值)如何注入Bean                         |
| GET       | /env            | 获取全部环境属性                                             |
| GET       | /env/{name}     | 根据名称获取特定的环境属性值                                 |
| GET       | /flyway         | 提供一份 Flyway 数据库迁移信息                               |
| GET       | /liquidbase     | 显示Liquibase 数据库迁移的纤细信息                           |
| GET       | /health         | 报告应用程序的健康指标，这些值由 HealthIndicator 的实现类提供 |
| GET       | /heapdump       | dump 一份应用的 JVM 堆信息                                   |
| GET       | /httptrace      | 显示HTTP足迹，最近100个HTTP request/repsponse                |
| GET       | /info           | 获取应用程序的定制信息，这些信息由info打头的属性提供         |
| GET       | /logfile        | 返回log file中的内容(如果 logging.file 或者 logging.path 被设置) |
| GET       | /loggers        | 显示和修改配置的loggers                                      |
| GET       | /metrics        | 报告各种应用程序度量信息，比如内存用量和HTTP请求计数         |
| GET       | /metrics/{name} | 报告指定名称的应用程序度量值                                 |
| GET       | /scheduledtasks | 展示应用中的定时任务信息                                     |
| GET       | /sessions       | 如果我们使用了 Spring Session 展示应用中的 HTTP sessions 信息 |
| POST      | /shutdown       | 关闭应用程序，要求endpoints.shutdown.enabled设置为true       |
| GET       | /mappings       | 描述全部的 URI路径，以及它们和控制器(包含Actuator端点)的映射关系 |
| GET       | /threaddump     | 获取线程活动的快照                                           |

默认只暴露`/actuator/health`和`/actuator/info`

打开所有端点：

```yaml
management:
  endpoint:
    health:
      show-details: always
  endpoints:
    web:
      exposure:
        include: '*'
```

或者选择打开指定端点：

```yaml
  endpoints:
    web:
      exposure:
        include: ['beans','env','health']
```

