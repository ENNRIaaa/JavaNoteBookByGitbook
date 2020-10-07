# Lombok

使用Lombok需要安装插件，并引入依赖，这里不做介绍。

主要介绍几个注解的使用，[更多注解使用](https://projectlombok.org/features/all)

```java
package com.itmuch.usercenter;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
import lombok.extern.slf4j.Slf4j;

@Slf4j
public class LombokTest {

    public static void main(String[] args) {
        UserRegisterDTO dto = UserRegisterDTO.builder()
                .email("xxx")
                .password("123")
                .confirmPassword("123")
                .build();
        log.info("构造出来的UserRegisterDTO={}", dto);
    }
}

@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
class UserRegisterDTO {
    private String email;
    private String password;
    private String confirmPassword;
}
```



> @Slf4j

自动生成private static final org.slf4j.Logger log对象，打印日志

> @Builder

构造者模式，链式创建对象

> @RequiredArgsConstructor

为final修饰和`@NonNull`修饰的成员属性生成构造器

```java
@RequiredArgsConstructor
public class NacosSameClusterWeightedRule extends AbstractLoadBalancerRule {
		
    // 通过带参构造器实现自动注入，无需@Autowired
    private final NacosDiscoveryProperties nacosDiscoveryProperties;
```

