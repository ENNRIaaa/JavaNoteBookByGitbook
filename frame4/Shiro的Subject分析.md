# 5.29 Shiro的Subject分析

#### 解读官方的十分钟快速开始：

通过`SecurityUtils`获取Subject对象，得到当前User

```java
Subject currentUser = SecurityUtils.getSubject();
```



通过当前User获取Session对象

```java
Session session = currentUser.getSession();
```



session存值取值：

```java
session.setAttribute("someKey", "aValue");
String value = (String) session.getAttribute("someKey");
```



判断当前User是否被认证：

```java
// 被认证返回true
currentUser.isAuthenticated()
```



通过用户名密码生成令牌token：

```java
UsernamePasswordToken token = new UsernamePasswordToken("lonestarr", "vespa");
token.setRememberMe(true);// 还可以设置记住我
```



通过令牌登陆：

```java
currentUser.login(token);
```



得到当事人（登陆用户名）：

*如果当前User没有被认证（没登录），则返回null*

```java
currentUser.getPrincipal()
```



判断当前用户是否有XXX角色：

```java
// 认证（角色）
currentUser.hasRole("schwartz")
```



判断当前用户是否有XXX许可：

```java
// 授权（许可）
currentUser.isPermitted("lightsaber:wield")
```



注销：

```java
currentUser.logout();
```



---

***了解了Shiro的基础对象之后，接下来要完成SpringBoot整合Shiro***