# 5.32 Shiro实现用户认证

首先，在控制类中定义登陆的处理方法：

```java
@PostMapping("/login")
public String login(String username,String password,Model model){
  Subject currentUser = SecurityUtils.getSubject();
  UsernamePasswordToken token = new UsernamePasswordToken(username, password);
  try{
    currentUser.login(token);
    return "index";
  }catch (UnknownAccountException une){
    model.addAttribute("msg","用户名不存在");
  }catch (IncorrectCredentialsException ice){
    model.addAttribute("msg","密码错误");
  }
  return "login";
}
```

- 通过`SecurityUtils.getSubject();`获取Subject对象，当前用户(currentUser)
- 通过用户名密码生成令牌(token)
- `currentUser.login(token);`，通过令牌登陆，执行这行代码时，就会调用`UserRealm`类中的`doGetAuthenticationInfo`方法，这个方法具体内容在下面。
- 如果`UserRealm`类中的认证方法认证通过，`return "index";`返回首页
- 如果认证没有通过，`UserRealm`类认证方法会抛出异常，控制类这里接收相应异常，返回错误消息(msg)到前端页面



然后，编写`UserRealm`中的认证方法：

```java
/**
     * 认证
     * @param token
     * @return
     * @throws AuthenticationException
     */
@Override
protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
  System.out.println("执行了认证 doGetAuthenticationInfo()");
  //做一个临时的用户名和密码（正常要从数据库获取）
  String user = "admin";
  String pass = "123";

  //如果登陆的用户名和内存中的用户名不一致，返回null抛出异常
  if(!token.getPrincipal().equals(user)){
    return null;
  }
  //返回SimpleAuthenticationInfo，校验密码
  return new SimpleAuthenticationInfo("",pass,"");
}
```



---

***完成这一步可以实现的效果：点击添加或者修改会自动跳转到登陆页面，登陆的用户名或密码错误会提示相应信息，登陆正确会跳转到首页，点击添加或修改可以正常访问。***

