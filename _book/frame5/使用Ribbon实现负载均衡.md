# 使用Ribbon实现负载均衡

> Ribbon是Netflix开源的客户端侧负载均衡器



### Step1 添加依赖

`spring-cloud-starter-alibaba-nacos-discovery`组件已经包含了Ribbon，所以无需添加依赖



### Step2 写注解

```java
@Bean
@LoadBalanced
public RestTemplate restTemplate(){
  return new RestTemplate();
}
```

要在RestTemplate上添加`@LoadBalanced`注解，为RestTemplate整合Ribbon



### Step 改写Service方法

```java
@Slf4j
@Service
@RequiredArgsConstructor
public class ShareService {

    private final ShareMapper shareMapper;
    private final RestTemplate restTemplate;

    public ShareDTO findById(Integer id) {
        // 获取分享详情
        Share share = this.shareMapper.selectByPrimaryKey(id);
        // restTemplate已经整合了Ribbon，Ribbon会根据要请求的服务名称自动从服务发现中心获取所有的实例，再根据负载均衡算法进行请求
        UserDto userDto = this.restTemplate.getForObject("http://user-center/users/{id}", UserDto.class, share.getUserId());
        // 消息装配
        ShareDTO shareDTO = new ShareDTO();
        BeanUtils.copyProperties(share, shareDTO);
        shareDTO.setWxNickname(userDto.getWxNickname());
        return shareDTO;
    }
}
```

