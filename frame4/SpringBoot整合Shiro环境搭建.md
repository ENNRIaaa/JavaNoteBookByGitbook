# 5.30 SpringBoot整合Shiro环境搭建

1. 导入Shiro-SpringBoot整合依赖：

   ```xml
   <dependency>
     <groupId>org.apache.shiro</groupId>
     <artifactId>shiro-spring-boot-starter</artifactId>
     <version>1.5.3</version>
   </dependency>
   ```

2. 创建config包，自定义UserRealm类，继承`AuthorizingRealm`：

   重写下面这两个方法，一个是用于授权的，一个是用于认证的
   
   ```java
   public class UserRealm extends AuthorizingRealm {
   		// 授权
       @Override
       protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principals) {
           return null;
       }
   
   		// 认证 
       @Override
       protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
           return null;
       }
   }
   ```
   
3. 在config下创建ShiroConfig配置类：

   依次注册：`UserRealm`->`DefaultWebSecurityManager`->`ShiroFilterFactoryBean`到容器：

   ```java
   @Configuration
   public class ShiroConfig {
   
   		// ShiroFilterFactoryBean
       @Bean
       public ShiroFilterFactoryBean shiroFilterFactoryBean(@Autowired DefaultWebSecurityManager securityManager){
           // 设置安全管理器
           ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
           bean.setSecurityManager(securityManager);
           return bean;
       }
   
   		// DefaultWebSecurityManager
       @Bean
       public DefaultWebSecurityManager securityManager(@Autowired UserRealm userRealm){
           DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
           // 关联UserRealm
           securityManager.setRealm(userRealm);
           return securityManager;
       }
   
   		// realms
       @Bean
       public UserRealm userRealm(){
           return new UserRealm();
       }
   }
   ```

   