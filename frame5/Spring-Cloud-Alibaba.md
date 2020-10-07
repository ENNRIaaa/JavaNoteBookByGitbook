# Spring Cloud Alibaba

## 什么是Spring Cloud

- 快速构建分布式系统的工具集

  <table>
  	<tr>
    	<th>功能</th>
      <th>翻译</th>
      <th>选择</th>
    </tr>
    	<tr>
    	<td>Distributed/versioned<br>discovery</td>
      <td>分布式/版本化的配置<br>管理</td>
        <td>Spring Cloud Config、Consul、<b>Nacos</b>、Zookeeper</td>
    </tr>
    <tr>
    	<td>Service registration and discovery</td>
      <td>服务注册与发现</td>
      <td>Eureka、Consul、<b>Nacos</b>、Zookeeper</td>
    </tr>
    <tr>
    	<td>Routing</td>
      <td>路由</td>
      <td>Zuul、Spring Cloud Gateway</td>
    </tr>
    <tr>
    	<td>Service-to-service calls</td>
      <td>端到端的调用</td>
      <td><b>RestTeamplate</b><b>Feign</b></td>
    </tr>
    <tr>
    	<td>Load balancing</td>
      <td>负载均衡</td>
      <td><b>Ribbon</b></td>
    </tr>
    <tr>
    	<td>Circuit Breakers</td>
      <td>断路由</td>
      <td>Hystrix、<b>Sentinel</b>、Resilience4j</td>
    </tr>
    <tr>
    	<td>Global locks</td>
      <td>全局锁</td>
      <td>Spring Cloud Cluster（以迁移到Spring Integration）</td>
    </tr>
    <tr>
    	<td>Leadership election and cluster state</td>
      <td>选举与集群状态管理</td>
      <td>Spring Cloud Cluster（已迁移到Spring Integration）</td>
    </tr>
    <tr>
    	<td>Distributed messaging</td>
      <td>分布式消息</td>
      <td>Spring Cloud Stream + kafka/RabbitMQ/<b>RocketMQ</b></td>
    </tr>
  </table>

- Spring Cloud常用子项目

  ![image-20200819234015100](https://images.shiguangping.com/imgs/20200819234015.png)



## 什么是Spring Cloud Alibaba

- Spring Cloud Alibaba是Spring Cloud的子项目

- 致力于提供微服务开发的一站式解决方案。

  - 包含微服务开发的必备组件
  - 基于Spring Cloud，符合Spring Cloud标准
  - 阿里的微服务解决方案

  <table>
  	<tr>
    	<th>功能</th>
      <th>产品</th>
      <th>备注</th>
    </tr>
    	<tr>
    	<td>服务限流降级</td>
      <td><b>Sentinel</b></td>
      <td>开源组件</td>
    </tr>
      </tr>
    	<tr>
    	<td>服务注册与发现</td>
      <td><b>Nacos</b><br>ANS</td>
      <td>开源组件<br>商业组件</td>
    </tr>
  <tr>
  	<td>分布式配置管理</td>
    <td><b>Nacos</b><br>ACM</td>
    <td>开源组件<br>商业组件</td>
  </tr>
  <tr>
  	<td>消息驱动能力</td>
    <td><b>Spring Cloud Stream</b><br>RocketMQ</td>
    <td>开源组件</td>
  </tr>
  <tr>
  	<td>分布式事务</td>
    <td>Seata</td>
    <td>开源组件，不能用于生产(目前0.6.1)，1.0.0之后才可用于生产</td>
  </tr>
  <tr>
  	<td>阿里云对象存储</td>
    <td>OSS</td>
    <td>商业组件</td>
  </tr>
  <tr>
  	<td>分布式任务调度</td>
    <td>SchedulerX</td>
    <td>商业组件</td>
  </tr>
  <tr>
  	<td>阿里云短信服务</td>
    <td>SMS</td>
    <td>商业组件</td>
  </tr>
  </table>
  
  

---

## 版本与兼容性

### Spring Cloud版本问题

由于Spring Cloud有众多子项目，每个子项目又有自己的版本控制，所有Spring Cloud搞了一个发布列车Release Trains，每一代的Spring Cloud版本只有名称，而没有具体的版本号。

Spring Cloud每一代版本使用伦敦地铁站命名，按字母顺序往后排。

历代版本：

- Angel
- Brixton
- Camden
- Dalston
- Edgware
- Finchley
- Greenwich
- Hoxton

每一代版本又有Service Release（SR）版本，主要是修复各种bug。Hoxton SR7就是Hoxton的第七个bug修复版本

每一代版本的顺序是这样子的：Hoxton RELEASE -> Hoxton SR1 -> Hoxton SR2



### Spring Cloud生命周期

Spring Cloud版本发布规划[https://github.com/spring-cloud/spring-cloud-release/milestones](https://github.com/spring-cloud/spring-cloud-release/milestones)

Spring Cloud版本发布记录[https://github.com/spring-cloud/spring-cloud-release/releases](https://github.com/spring-cloud/spring-cloud-release/releases)

Spring Cloud版本终止声明[https://spring.io/projects/spring-cloud#overview](https://spring.io/projects/spring-cloud#overview)



### Spring Boot、Spring Cloud、Spring Cloud Alibaba兼容性关系

[https://github.com/alibaba/spring-cloud-alibaba/wiki/版本说明](https://github.com/alibaba/spring-cloud-alibaba/wiki/版本说明)

| Spring Cloud Version        | Spring Cloud Alibaba Version      | Spring Boot Version |
| --------------------------- | --------------------------------- | ------------------- |
| Spring Cloud Hoxton.SR3     | 2.2.1.RELEASE                     | 2.2.5.RELEASE       |
| Spring Cloud Hoxton.RELEASE | 2.2.0.RELEASE                     | 2.2.X.RELEASE       |
| Spring Cloud Greenwich      | 2.1.2.RELEASE                     | 2.1.X.RELEASE       |
| Spring Cloud Finchley       | 2.0.2.RELEASE                     | 2.0.X.RELEASE       |
| Spring Cloud Edgware        | 1.5.1.RELEASE(停止维护，建议升级) | 1.5.X.RELEASE       |



### 生产环境怎么选择版本

- 坚决不用非稳定版本/end-of-life版本
- 尽量用最新一代
  - XXX.RELEASE版本缓一缓
  - SR2之后一般可以大规模使用

---

## 为项目整合Spring Cloud Alibaba

pom.xml中添加依赖：

```xml
<dependencyManagement>
  <dependencies>
    <!-- 整合Spring Cloud -->
    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-dependencies</artifactId>
      <version>Hoxton.SR7</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
    <!-- 整合Spring Cloud Alibaba -->
    <dependency>
      <groupId>com.alibaba.cloud</groupId>
      <artifactId>spring-cloud-alibaba-dependencies</artifactId>
      <version>2.2.1.RELEASE</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

*Spring Cloud Alibaba是基于Spring Cloud的，根据Spring Cloud版本不同，对应Spring Cloud Alibaba的版本也不同，具体的依赖关系，查看[https://github.com/alibaba/spring-cloud-alibaba/wiki/版本说明](https://github.com/alibaba/spring-cloud-alibaba/wiki/版本说明)*

