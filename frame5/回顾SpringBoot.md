# 回顾Spring Boot

## Spring Boot是什么？能做什么？

- 是一个快速开发的脚手架，类似Vue-Cli一样
- 作用：快速创建独立的、生产级的基于Spring的应用程序
- 特性：
  - 无需部署war文件
  - 提供Starter简化配置，开箱即用
  - 尽可能自动配置Spring以及第三方库
  - 提供“生产就绪”功能，例如指标、健康检查、外部配置等
  - 无代码生成、无XML

---

## 创建Spring Boot应用

Spring提供了Initializr快速创建SpringBoot应用程序，[https://start.spring.io/](https://start.spring.io/)。大多数IDEA也集成了该功能。

每一个SpringBoot应用都有一个启动类，启动类中提供了一个Main方法，这是SpringBoot应用启动的入口。

创建完项目，添加依赖之后，可以使用Maven命令构建项目，确保构建成功后再启动：

```bash
maven clean install
```

项目构建成功之后，会在`target`目录下生成编译好的jar包，通过`java -jar`执行jar包：

```bash
java -jar spring-boot-demo-0.0.1-SNAPSHOT.jar
```

---

## Spring Boot应用的组成

1. pom.xml文件，用来配置Maven依赖
2. 启动类，启动类的注解`@SpringBootApplication`
3. 配置文件：`application.properties`或者`application.yaml`，后者是Spring官方推荐的。
4. static目录，用来存放静态文件
5. templates目录，用来存放模板文件，Spring Boot支持的模板引擎：
   - FreeMarker
   - Groovy
   - Thymeleaf
   - Mustache

---

## Spring Boot开发三板斧

1. 加依赖
2. 写注解
3. 写配置