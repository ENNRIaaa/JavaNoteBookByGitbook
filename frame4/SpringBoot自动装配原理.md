# SpringBoot自动装配原理

**pom.xml：**

父项目：

```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>2.3.1.RELEASE</version>
  <relativePath/> <!-- lookup parent from repository -->
</parent>
```

进入父项目可以看到父项目的父项目：

```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-dependencies</artifactId>
  <version>2.3.1.RELEASE</version>
</parent>
```

它来真正管理Spring Boot所有依赖的版本，我们正常导入依赖是不需要指定版本的，但是没有在这个爷爷项目中管理的依赖，导入则需要指定版本。



**pom中的启动器：**

```xml
<!--启动器-->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter</artifactId>
</dependency>
```

- 启动器：就是SpringBoot的启动场景，如spring-boot-starter-web，它会帮我们导入web环境的所有依赖

- SpringBoot中将所有的功能场景，都变成一个个启动器

- 如果我们要使用什么功能，只需要找到对应的启动器就可以了，所有**官方**启动器都遵循类似的命名方式。`spring-boot-starter-*`，其中`*`是特定类型的应用程序。



**主程序：**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

//标注这个类是一个SpringBoot应用：启动类下的所有资源被导入
@SpringBootApplication
public class Springboot01HelloworldApplication {
  //将SpringBoot应用启动
  public static void main(String[] args) {
    SpringApplication.run(Springboot01HelloworldApplication.class, args);
  }
}
```

- @SpringBootApplication 注解：标注这个类是一个SpringBoot的应用，这个注解又被其它注解修饰，其中有两个核心的注解：

  ```java
  @SpringBootConfiguration ：SpringBoot的配置
  	- @Configuration ：Spring配置类
  		- @Component ：说明这也是一个Spring组件
  
  @EnableAutoConfiguration：自动配置
  	- @AutoConfigurationPackage：自动配置包
  		-@Import(AutoConfigurationPackages.Registrar.class)：自动配置包
  	- @Import(AutoConfigurationImportSelector.class)：自动配置导入选择器
  
  //获取所有配置
  List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);
  ```

  获取候选的配置：

  ```java
  protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
    List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),
                                                                         getBeanClassLoader());
    Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you "
                    + "are using a custom packaging, make sure that file is correct.");
    return configurations;
  }
  ```

  META-INF/spring.factories：自动配置的核心文件

  ![image-20200627230638135](https://images.shiguangping.com/imgs/20200627230638.png)

#### 流程分析：

![image-20200629122303959](https://images.shiguangping.com/imgs/20200629122304.png)



结论：SpringBoot所有自动配置都是在启动的时候扫描并加载`spring.factories`，所有的自动配置类都在这里面，但是不一定生肖，要判断条件是否成立。只要导入了对应的`start`，就有对应的启动器了，有了启动器，我们自动装配就会生效，然后配置成功。

1. SpringBoot在启动的时候，从类路径下`/META-INF/spring.factories`获取指定的值
2. 将这些自动配置的类导入容器，自动配置就会生效，帮我们进行自动配置
3. 以前我们需要配置的东西，现在SpringBoot都帮我们做了
4. 整合JavaEE，解决方案和自动配置的东西都在`spring-boot-autoconfigure-2.3.1.RELEASE.jar`包下
5. 它会把所有需要导入的组件，以类名的方式返回，这些组件就会被添加到容器中
6. 容器中也会存在非常多的XxxAutoConfiguration的文件(@Bean)，就是这些类给容器中导入了这个场景需要的所有组件并自动配置，@Configuration，JavaConfig
7. 有了自动配置类，免去了我们手动编写配置文件的工作。



### 主启动类

```java
package com.neu;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Springboot01HelloworldApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot01HelloworldApplication.class, args);
    }
}
```

#### class SpringApplication

这个类主要做了以下四件事清：

- 推断应用的类型是普通的项目还是Web项目
- 查找并加载所有可用的初始化器，设置到initializers属性中
- 找出所有的应用程序监听器，设置到listeners属性中
- 推断并设置main方法的定义类，找到运行的主类