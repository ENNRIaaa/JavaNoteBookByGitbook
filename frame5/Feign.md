# Feign

> Feign是Netflix开源的声明式HTTP客户端

三板斧的第一步，添加Feign依赖：

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```



## Feign的组成

<table>
	<tr>
  	<th>接口</th>
    <th>作用</th>
    <th>默认值</th>
  </tr>
  <tr>
  	<td>Feign.Builder</td>
    <td>Feign的入口</td>
    <td>Feign.Builder</td>
  </tr>
  <tr>
    <td>Client</td>
  	<td>Feign底层用什么去请求</td>
    <td>和Ribbon配合时：LoadBalancerFeignClient<br>不和Ribbon配合时：feign.Client.Default</td>
  </tr>
  <tr>
  	<td>Contract</td>
    <td>契约，注解支持</td>
    <td>SpringMvcContract</td>
  </tr>
  <tr>
  	<td>Encoder</td>
    <td>编码器，用于将对象转换成HTTP请求消息体</td>
    <td>SpringEncoder</td>
  </tr>
  <tr>
  	<td>Decoder</td>
    <td>解码器，将响应消息体转换成对象</td>
    <td>ResponseEntityDecoder</td>
  </tr>
  <tr>
  	<td>Logger</td>
    <td>日志管理器</td>
    <td>Slf4jLogger</td>
  </tr>
  <tr>
  	<td>RequestInterceptor</td>
    <td>用于为每个请求添加通用逻辑</td>
    <td>无</td>
  </tr>
</table>
注意：

Feign不和Ribbon搭配使用时，底层使用的是`Client.Default`去请求，Default默认用的`HttpURLConnection`去请求，`HttpURLConnection`是没有连接池的。

Feign在和Ribbon使用时，底层使用`LoadBalancerFeignClient`请求，它应用了代理模式，在默认情况下，也是使用的Client.Default去请求的。



## 自定义Feign日志级别

<table>
	<tr>
  	<th>级别</th>
    <th>打印内容</th>
  </tr>
  	<tr>
  	<td>NONE（默认值）</td>
    <td>不记录任何日志</td>
  </tr>
  	<tr>
  	<td>BASIC</td>
    <td>仅记录请求方法、URL、响应状态代码以及执行时间</td>
  </tr>
  	<tr>
  	<td>HEADERS</td>
    <td>几率BASIC级别的基础上，几率请求和响应的header</td>
  </tr>
  	<tr>
  	<td>FULL</td>
    <td>记录请求和响应的header、body和元数据</td>
  </tr>
</table>


## 细粒度配置自定义

**Java Config方式：**

1. 在`@FeignClient`注解中添加configuration属性，指向Feign的自定义配置类。

   ```java
   @FeignClient(name = "user-center",configuration = UserCenterFeignConfiguration.class)
   public interface UserCenterFeignClient {
   
       @GetMapping("/users/{id}")
       UserDto findById(@PathVariable("id") Integer id);
   }
   ```

2. 自定义配置类Feign配置类，定义日志界别。

   *Feign配置类不要加`@Configutation`注解，或者把这个类移到启动类扫描不到的位置。否则该配置类会被所有的FeignClient共享。*

   ```java
   public class UserCenterFeignConfiguration {
       @Bean
       public Logger.Level level(){
           return Logger.Level.FULL;
       }
   }
   ```

3. 在配置文件中配置Feign接口的全路径，日志级别必须是**debug**

   ```yaml
   logging:
     level:
       com.example.contentcenter.feignclient.UserCenterFeignClient: debug
   ```

   

**配置文件方式：**

使用配置文件方式配置Feign的日志级别，不需要在`@FeignClient`注解添加configuration属性。只需要在配置文件中直接定义Feign的日志级别即可：

```yaml
feign:
  client:
    config:
      # 要访问的服务名称
      user-center:
        # Feign的日志级别
        loggerLevel: full
```



## 全局配置

**Java Config方法：**

- ~~方式一：让父子上下文ComponentScan重叠（强烈不建议使用）~~

- 方式二：【唯一正确的途径】：

  启动类中`@EnableFeignClients(defaultConfiguration=xxx.class)`注解添加defaultConfiguration属性，该属性定义全局配置类。

  在全局配置类中定义日志级别：
  
  ```java
  public class GlobalFeignConfiguration {
      @Bean
      public Logger.Level level(){
          return Logger.Level.FULL;
      }
  }
  ```
  
  

**配置文件方法：**

```yaml
feign:
  client:
    config:
      # 服务名称改为default，则启用全局配置
      default:
        # Feign的日志级别
        loggerLevel: full
```



## 支持的配置项

- 支持的配置项-代码方式

  <table>
    <tr>
    	<th>配置项</th>
      <th>作用</th>
    </tr>
  	<tr>
    	<td>Logger.Level</td>
      <td>指定日志级别</td>
    </tr>
    <tr>
    	<td>Retryer</td>
      <td>指定重试策略</td>
    </tr>
    <tr>
      <td>ErrorDecoder</td>
    	<td>指定错误解码器</td>
    </tr>
    <tr>
    	<td>Request.Options</td>
      <td>超时时间</td>
    </tr>
    <tr>
    	<td>Collection<RequestInterceptor></td>
      <td>拦截器</td>
    </tr>
    <tr>
    	<td>SetterFactory</td>
      <td>用于设置Hystrix的配置属性，Feign整合Hystrix才会用</td>
    </tr>
  </table>

- 支持的配置项-属性方式

  ```yaml
  feign:
    client:
      config:
        <feignName>:
          connectTimeout: 5000   # 连接超时时间
          readTimeout: 5000      # 读取超时时间
          loggerLevel: full      # 日志级别
          errorDecoder: com.example.SimpleErrorDecoder    # 错误解码器
          retryer: com.example.SimpleRetryer              # 重试策略
          requestInterceptors:
            - com.example.FoorRequestInterceptor          # 拦截器
          # 是否对404错误码解码
          # 处理逻辑相减feign.SynchronousMethodHandler#executeAndDecode
          decode404: false
          encoder: com.example.SimpleEncoder    # 编码器
          decoder: com.example.SimpleDecoder    # 解码器
          contract: com.example.SimpleContract  # 契约
  ```



**Ribbon配置 vs Feign配置：**

- Ribbon代码方式：
  - 局部：`@RibbonClient(configuration=X.class)`X必须加@Configuration注解，且必须放在父上下文无法扫描到的包中
  - 全局`@RibbonClients(defaultConfiguration)`
- Ribbon属性方式：
  - 局部：`<clientName>.ribbon.NFLoadBalancerClassName`, ...
  - 全局：-
- Feign代码方式：
  - 局部：`@FeignClient(configuration=Y.class)`Y的@Configuration可选，如果有，必须放在父上下文无法扫描到的包
  - 全局：`@EnableFeignClients(defaultConfiguration)`
- Feign属性方式：
  - 局部：`feign.client.config.<clientName>.loggerLevel`, ...
  - 全局：`feign.client.config.default.loggerLevel`, ...

**Feign代码方式 vs 属性方式：**

<table>
	<tr>
  	<th>配置方式</th>
    <th>优点</th>
    <th>缺点</th>
  </tr>
  	<tr>
  	<td>代码配置</td>
    <td>基于代码，更加灵活</td>
    <td>如果Feign的配置类加了@Configuration注解，需要注意父子上下文<br>线上修改得重新打包、发布</td>
  </tr>
    	<tr>
  	<td>属性配置</td>
    <td>易上手<br>配置更加直观<br>线上修改无需重新打包、发布<br>优先级更高：<br><b>全局代码>全局属性>细粒度代码>细粒度属性</b></td>
    <td>极端场景下没有代码配置方式灵活</td>
  </tr>
</table>



**最佳实践：**

- 尽量使用属性配置，属性方式实现不了的情况下再考虑用代码配置
- 在同一个微服务内尽量保持单一性，比如统一使用属性配置，不用两种方式混用，增加定位代码的复杂性



## Feign脱离Ribbon的使用方式

Feign脱离Ribbon使用，可以使用Feign访问没有在Nacos注册的服务，例如访问百度，代码示例：

```java
@FeignClient(name = "baidu", url = "https://www.baidu.com/")
public interface TestBaiduFeignClient {
    @GetMapping("")
    String index();
}
```

`@FeignClient(name = "baidu", url = "https://www.baidu.com/")`中name属性值可以任意，但是是必须定义的，url属性指向要请求的地址。

测试类：

```java
@Autowired
private TestBaiduFeignClient testBaiduFeignClient;

@GetMapping("baidu")
public String baiduIndex(){
  return this.testBaiduFeignClient.index();
}
```



## RestTemplate vs Feign

<table>
	<tr>
  	<th>角度</th>
    <th>RestTemplate</th>
    <th>Feign</th>
  </tr>
  	<tr>
  	<td>可读性、可维护性</td>
    <td>一般</td>
    <td>极佳</td>
  </tr>
    	<tr>
  	<td>开发体验</td>
    <td>欠佳</td>
    <td>极佳</td>
  </tr>
    	<tr>
  	<td>性能</td>
    <td>很好</td>
    <td>中等（RestTemplate的50%左右）</td>
  </tr>
    	<tr>
  	<td>灵活性</td>
    <td>极佳</td>
    <td>中等（内置功能可满足绝大多数需求）</td>
  </tr>
</table>

- 原则：尽量用Feign，杜绝使用RestTemplate
- 事无绝对，合理选择



## Feign的性能优化

- 配置连接池【提升15%左右】，Feign默认使用URLConnection进行请求，URLConnection是没有连接池的。

- 合适的日志级别，不建议用full，打印日志比较多，消耗性能。

  

  **配置带有连接池的http客户端：**

  apache的httpclient：添加依赖

  ```xml
  <dependency>
    <groupId>io.github.openfeign</groupId>
    <artifactId>feign-httpclient</artifactId>
  </dependency>
  ```

  写配置：

  ```yaml
  feign:
  	httpclient:
  		# 让feign使用apache httpclient做请求；而不是默认的URLConnection
  		enabled: true
  		# feign的最大连接数
      max-connections: 200
      # feign单个路径的最大连接数
      max-connections-per-route: 50
  ```

  或者，使用okhttp：添加依赖

  ```xml
  <dependency>
    <groupId>io.github.openfeign</groupId>
    <artifactId>feign-okhttp</artifactId>
    <version>10.1.0</version>
  </dependency>
  ```

  写配置：

  ```yaml
  feign:
  	okhttp:
  		# 让feign使用apache httpclient做请求；而不是默认的URLConnection
  		enabled: true
  		# feign的最大连接数
      max-connections: 200
      # feign单个路径的最大连接数
      max-connections-per-route: 50
  ```



