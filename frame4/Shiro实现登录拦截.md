# 5.31 Shiro实现登录拦截

#### 设置Shiro的过滤器：

Shiro常用过滤器：

- anon：无需认证即可访问
- authc：必须认证才能访问
- user：必须拥有【记住我】功能才能使用
- perms：拥有对某个资源的权限才能访问
- role：拥有有个角色权限才能访问



通过Shiro过滤器进行拦截请求，设置登陆Url，如果无访问权限，则跳到登录页面：

```java
/**
     * ShiroFilterFactoryBean
     * @return
     */
@Bean
public ShiroFilterFactoryBean shiroFilterFactoryBean(@Autowired DefaultWebSecurityManager securityManager){
  ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
  // 设置安全管理器
  bean.setSecurityManager(securityManager);

  // 添加Shiro的内置过滤器
  Map<String, String> filterMap = new LinkedHashMap<>();
  filterMap.put("/user/**","authc");
  bean.setFilterChainDefinitionMap(filterMap);

  // 设置登陆页面
  bean.setLoginUrl("/toLogin");

  return bean;
}
```



