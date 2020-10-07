# Profile

## 如何实现不同环境不同配置？

在yaml文件中，通过连字符("---")三个中划线来分割不同环境的配置：

```yaml
# 公共配置
# 监控
management:
  endpoint:
    health:
      show-details: ${SOME_ENV}
  endpoints:
    web:
      exposure:
        include: beans,env,health,configprops
# 用来描述应用
info:
  app-name: spring-boot-demo
  author: liyan
  mail: xxx@qq.com
# 激活
spring:
  profiles:
    active: prod

---
# 开发环境
spring:
  profiles: dev
server:
  port: 8081

---
# 生产环境
spring:
  profiles: prod
server:
  port: 8082
  tomcat:
    threads:
      max: 300
    max-connections: 1000
```

---

使用properties配置文件配置多套开发环境，需要创建多个配置文件。