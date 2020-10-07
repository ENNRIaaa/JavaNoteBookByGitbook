# Ribbon 负载均衡

负载均衡的两种实现：

- 服务器端负载均衡
- 客户端负载均衡

```java
public ShareDTO findById(Integer id) {
  Share share = this.shareMapper.selectByPrimaryKey(id);
	// 通过discoveryClient获取到服务提供者的所有实例
  List<ServiceInstance> instances = discoveryClient.getInstances("user-center");
  // 获得所有服务提供者实例的接口地址
  List<String> targetURLs = instances.stream()
    .map(instance -> instance.getUri().toString() + "/users/{id}")
    .collect(toList());
  // 通过targetURLs大小获得一个随机索引，通过随机索引随机访问服务提供者实例，实现负载均衡
  int index = ThreadLocalRandom.current().nextInt(targetURLs.size());
  UserDto userDto = this.restTemplate.getForObject(targetURLs.get(index), UserDto.class, share.getUserId());
  ShareDTO shareDTO = new ShareDTO();
  BeanUtils.copyProperties(share, shareDTO);
  shareDTO.setWxNickname(userDto.getWxNickname());
  return shareDTO;
}
}
```

通过在服务消费者获取到所有服务提供者实例，并随机调用（即客户端负载均衡）。

---

## Ribbon实现负载均衡

> Ribbon是Netflix开源的客户端侧负载均衡器

**添加依赖：**

`spring-cloud-starter-alibaba-nacos-discovery`组件已经包含了Ribbon，所以无需添加依赖

**写注解：**

RestTemplate整合Ribbon

```java
@Bean
@LoadBalanced
public RestTemplate restTemplate(){
  return new RestTemplate();
}
```

**修改Service方法：**

```java
public ShareDTO findById(Integer id) {
  Share share = this.shareMapper.selectByPrimaryKey(id);
  // restTemplate已经整合了Ribbon，Ribbon会根据要请求的服务名称自动从服务发现中心获取所有实例，再根据Ribbon内置的负载均衡算法进行请求
  UserDto userDto = this.restTemplate.getForObject("http://user-center/users/{id}", UserDto.class, share.getUserId());
  
  ShareDTO shareDTO = new ShareDTO();
  BeanUtils.copyProperties(share, shareDTO);
  shareDTO.setWxNickname(userDto.getWxNickname());
  return shareDTO;
}
```

---

## Ribbon的组成

<table>
	<tr>
  	<th>接口</th>
    <th>作用</th>
    <th>默认值</th>
  </tr>
  	<tr>
  	<td>IClientConfig</td>
    <td>读取配置</td>
    <td>DefaultClientConfigImpl</td>
  </tr>
  <tr>
  	<td>IRule</td>
    <td>负载均衡规则，选择实例</td>
    <td>ZoneAvoidanceRule</td>
  </tr>
  <tr>
  	<td>IPing</td>
    <td>筛选掉ping不同的实例</td>
    <td>Dummyping</td>
  </tr>
  <tr>
  	<td>ServerList<Server></td>
    <td>交给Ribbon的实例列表</td>
    <td><b>Ribbon</b>：ConfigurationBasedServerList<br><b>Spring Cloud  Alibaba</b>:NacosServerList</td>
  </tr>
  <tr>
  	<td>ServerListFilter<Server></td>
    <td>过滤掉不符合条件的实例</td>
    <td>ZonePreferenceServerListFilter</td>
  </tr>
  <tr>
  	<td>ILoadBalancer</td>
    <td>Ribbon的入口</td>
    <td>ZoneAwareLoadBalancer</td>
  </tr>
    <tr>
  	<td>ServerListUpdater</td>
    <td>更新交给Ribbon的List的策略</td>
    <td>PollingServerListUpdater</td>
  </tr>
</table>

---

## Ribbon内置的负载均衡规则

<table>
	<tr>
  	<th>规则名称</th>
    <th>特点</th>
  </tr>
  <tr>
  	<td>AvailabilityFilteringRule</td>
    <td>过滤掉一直连接失败的被标记为circuit tripped的后端Server，并过滤掉哪些高并发的后端Server或者使用一个AvailabilityPredicate来包含过滤server的逻辑，其实就是检查status里记录的各个Server的运行状态</td>
  </tr>
  <tr>
  	<td>BestAvailableRule</td>
    <td>选择一个最小的并发请求的Server，逐个考察Server，如果Server被tripped了，则跳过</td>
  </tr>
  <tr>
  	<td>RandomRule</td>
    <td>随机选择一个Server</td>
  </tr>
  <tr>
  	<td>ResponseTimeWeightedRule</td>
    <td>已废弃，作用同WeightedResponseTimeRule</td>
  </tr>
  <tr>
  	<td>RetryRule</td>
    <td>对选择的负载均衡策略机上重试机制，在一个配置时间段内当选择Server不成功，则一直尝试使用subRule的方式选择一个可用的server</td>
  </tr>
  <tr>
  	<td>RoundRobinRule</td>
    <td>轮询选择，轮询index，选择index对应位置的Server</td>
  </tr>
  <tr>
  	<td>WeightedResponseTimeRule</td>
    <td>根据响应时间加权，适应时间越长，权重约小，被选中的可能性越低</td>
  </tr>
  <tr>
  	<td>ZoneAvoidanceRule</td>
    <td>复合判断Server所Zone的性能和Server的可用性选择Server，在没有Zone的环境下，类似于轮询(RoundRobinRule)</td>
  </tr>
</table>

Ribbon默认使用的负载均衡策略是轮询(RoundRobinRule)。

自定义负载均衡策略的两种方式：

- Java Config
- 配置文件配置

**第一种：Java Config**

在启动类所在包的并列级别创建一个包->创建配置类，目录层级只要配置类不被Spring Boot启动类扫描到即可，这里涉及Spring的父子上下文问题：

```java
@Configuration
public class RibbonConfiguration {

    @Bean
    public IRule ribbonRule() {
      // 返回不同的策略实现类即可
        return new RandomRule();
    }
  	// 定义其他配置，如IPing
    @Bean
    public IPing ping() {
        return new PingUrl();
    }
```

在启动类所在目录下创建包->创建配置类：

```java
@Configuration
// name:要调用的服务名称 configuration:上面定义的配置类
@RibbonClient(name = "user-center",configuration = RibbonConfiguration.class)
public class UserCenterRibbonConfiguration {

}
```

重新应用后，会启用新的负载均衡规则。

**第二种：配置文件配置策略**

```yaml
user-center:
  ribbon:
    NFLoadBalancerRuleClassName: com.netflix.loadbalancer.RandomRule
```

为要调用的`user-center`服务设置负载均衡策略，配置文件配置无需再写上面的两个Java配置类。



### 代码配置Vs属性配置

<table>
<tr><th>配置方法</th><th>优点</th><th>缺点</th></tr>
  <tr><td>代码配置</td><td>基于代码，更加灵活</td><td>有小坑（Spring父子上下文），线上修改需要重新打包、发布</td></tr>
  <tr><td>属性配置</td><td>易上手，配置更加直观，线上修改无需重新打包、发布，优先级更高</td><td>极端场景下没有代码配置方式灵活</td></tr>
</table>

细粒度配置最佳实践总结：

- 尽量使用属性配置，属性方式实现不了的情况下再考虑使用代码配置
- 在同一个微服务内尽量保持单一性，比如统一使用属性配置，不要两种方式混用，增加定位代码的复杂性

### 配置属性方式

`<clientName>.ribbon`如下属性：

- `NFLoadBalancerClassName`:`ILoadBalancer`实现类
- `NFLoadBalancerRuleClassName`:`IRule`实现类
- `NFLoadBalancerPingClassName`:`IPing`实现类
- `NIWSServerListClassName`:`ServerList`实现类
- `NIWSServerListClassName`:`ServerListFilter`实现类



## 自定义负载均衡策略

**基于权重的负载均衡策略：**

```java
// 自定义类并继承AbstractLoadBalancerRule
public class NacosWeightedRule extends AbstractLoadBalancerRule {
    @Autowired
    private NacosDiscoveryProperties nacosDiscoveryProperties;
		
  	// AbstractLoadBalancerRule类中需实现两个抽象方法initWithNiwsConfig和choose
  	
  	// 读取配置文件，并初始化NacosWeightedRule
    @Override
    public void initWithNiwsConfig(IClientConfig iClientConfig) {
        
    }

    @Override
    public Server choose(Object o) {
        try {
          	// 负载均衡器实例对象
            BaseLoadBalancer loadBalancer = (BaseLoadBalancer) this.getLoadBalancer();
            // 想要请求的微服务的名称
            String name = loadBalancer.getName();
            // 拿到服务发现的相关API
            NamingService namingService = nacosDiscoveryProperties.namingServiceInstance();
            // 使用Nacos提供的基于权重的负载均衡算法，nacos client自动通过基于权重的负载均衡算法，给我们选择一个实例
            Instance instance = namingService.selectOneHealthyInstance(name);
            return new NacosServer(instance);
        } catch (NacosException e) {
            return null;
        }
    }
}
```

自定义负载均衡策略之后，需要配置该策略，以使配置生效。

**同一集群下的负载均衡策略：**

```java
public class NacosSameClusterWeightedRule extends AbstractLoadBalancerRule {
    @Autowired
    private NacosDiscoveryProperties nacosDiscoveryProperties;

    @Override
    public void initWithNiwsConfig(IClientConfig iClientConfig) {

    }

    @Override
    public Server choose(Object o) {
        try {
            // 获取配置文件中配置的集群名称
            String clusterName = nacosDiscoveryProperties.getClusterName();
          	// 负载均衡器实例对象
            BaseLoadBalancer loadBalancer = (BaseLoadBalancer) this.getLoadBalancer();
            // 想要请求的微服务名称
            String name = loadBalancer.getName();
            // 拿到服务发现的相关API
            NamingService namingService = nacosDiscoveryProperties.namingServiceInstance();

            // 1.找到指定服务的所有实例 true表示只获取健康实例
            List<Instance> instances = namingService.selectInstances(name, true);
            // 2.根据配置文件中的集群名称过滤出相同集群下的所有实例
            List<Instance> sameClusterInstances = instances.stream()
                    .filter(instance -> Objects.equals(instance.getClusterName(), clusterName))
                    .collect(Collectors.toList());

            // 将要调用的实例列表放到该集合中
            List<Instance> instanceToBeChosen = new ArrayList<>();
          	// 3.如果该集群下没有实例，则调用其它集群下的实例
            if (CollectionUtils.isEmpty(sameClusterInstances)) {
                instanceToBeChosen = instances;
            } else {
              // 同一集群下有可用实例，则调用该集群下的实例
                instanceToBeChosen = sameClusterInstances;
            }
            // 4.基于权重的负载均衡算法，返回一个实例
            Instance instance = ExtendBalancer.getHostByRandomWeight1(instanceToBeChosen);
            return new NacosServer(instance);
        } catch (NacosException e) {
            return null;
        }
    }
}
// 调用Nacos的负载均衡方法：自定义类继承Balancer调用getHostByRandomWeight返回一个服务实例
class ExtendBalancer extends Balancer {
    public static Instance getHostByRandomWeight1(List<Instance> hosts) {
        return getHostByRandomWeight(hosts);
    }
}
```

Nacos已经有了基于权重的负载均衡算法，为什么还要整合Ribbon呢？主要是为了满足符合Spring Cloud的标准。

Spring Cloud有一个子项目叫`spring cloud commons`-->定义了Spring Cloud的标准

它其中又有一个子项目叫`spring cloud loadbalancer`-->定义了各种负载均衡的规则，没有权重这一概念，所以Spring Cloud Alibaba整合Ribbon，因为Ribbon符合Spring Cloud的负载均衡标准。



## 饥饿加载

Ribbon默认是懒加载，即请求服务的时候，采去加载Ribbon，所以第一次请求会很慢。开启饥饿加载后无论是否请求都会加载Ribbon。

```yaml
# ribbon饥饿加载
ribbon:
  eager-load:
    enabled: true
    clients: user-center
```



---

集群、元数据、命名空间待更新~