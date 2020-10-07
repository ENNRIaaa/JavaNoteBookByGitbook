# **Intellij IDEA中Mybatis Mapper自动注入警告的6种解决方案**

相信使用Mybaits的小伙伴们一定会经常编写类似如下的代码：

![IDEA mybatis警告](https://images.shiguangping.com/imgs/20200819002844.png)

可以看到 `userMapper` 下有个红色警告。虽然代码本身并没有问题，能正常运行，但有个警告总归有点恶心。本文分析原因，并列出解决该警告的几种方案。


## 原因

众所周知，IDEA是非常智能的，它可以理解Spring的上下文。然而 `UserMapper` 这个接口是Mybatis的，IDEA理解不了。

而 `@Autowired` 注解，默认情况下要求依赖对象（也就是 `userMapper` ）必须存在。而IDEA认为这个对象的实例/代理是个null，所以就**友好地给个提示**。

## 解决方案

### 方法1：为 `@Autowired` 注解设置required = false

使用 `@Autowired` 注解时，若希望允许null值，可设置required = false，像这样：

```java
@Autowired(required = false)
private UserMapper userMapper;
```

这样就不会有警告了。原因很好理解：IDEA认为userMapper是个null，给了警告；加上required = false后，使用 `@Autowired` 注解不再去校验userMapper是否存在了。也就不会有警告了。

**总结**：这种方式有点蛋疼。一个庞大的既有项目，可能到处都在引用Mapper，总不能到处都补上 required = false 吧……而且对于新手/新员工，很难一眼看懂加required = false属性只是为了解决IDEA的警告。

### 方法2：用 `@Resource` 替换 `@Autowired`

像这样：

```java
@Resource
private UserMapper userMapper;
```

这样也不会再有讨厌的警告。如果你对原因感兴趣，不妨了解一下[《@Autowired 与@Resource的区别》](https://blog.csdn.net/weixin_40423597/article/details/80643990)

**总结**：这种方式挺赞，但如果一个项目已经大量使用@Autowired，然后为了个警告到处改成@Resource，也有点蛋疼。

### 方法3：在Mapper接口上加上@Repository注解

像这样：

```java
@Repository
public interface UserMapper extends Mapper<User> {
}
```

这样也能让你的

```java
@Autowired
private UserMapper userMapper;
```

不再报错。

当然，如果你用@Component替换@Repository也是可以的。原理大致：IDEA不是认为 `userMapper` 是个null嘛…加个@Repository注解骗一下IDEA就OK了……

**总结**：这种方式比较赞，改动小，也简单，我比较喜欢。

### 方法4：用Lombok

像这样：

```java
@Service
@RequiredArgsConstructor(onConstructor = @__(@Autowired))
public class TestService {
    private final UserMapper userMapper;
    ...
}
```

Lombok生成的代码是这样的：

```java
@Service
public class TestService {
    private final UserMapper userMapper;
    @Autowired
    public TestService(final UserMapper userMapper) {
        this.userMapper = userMapper;
    }
    ...
}
```

**但如果自己手写成Lombok生成的代码，IDEA依然会给你报警告** 。我猜，应该是IDEA的Lombok插件把IDEA搞懵逼了…所以不提示了…

**总结** ：**这是我目前最喜欢的方式**。原因有2：

- Spring官方并不建议直接在类的field上使用@Autowired注解，原因详见：[《Why field injection is evil》](http://olivergierke.de/2013/11/why-field-injection-is-evil/) ，用本方法可将field注入编程构造方法注入，Spring是比较推荐的。
- 体现了Lombok的优势，简化了你的代码。而且你也不用在每个field上都加上@Autowired注解了。

**不过这种方式也有缺点**：那就是如果你类之间的依赖关系比较复杂，特别是存在循环依赖(A引用B，B引用A，或者间接的循环引用)时，应用将会启动不起来……**这其实是构造方法注入方式的缺点**。

### 方法5：把IDEA的警告关闭掉

个人没试过，也没有动力去试。没有提示的IDEA是没有灵魂的，我从来不去修改IDEA的任何警告设置。

### 方法6：安装mybatis plugin

安装mybatis plugin即可解决该问题。

## 总结

以上是解决问题的6种方法。问题本身其实比较简单，**但其实隐藏的知识点其实挺多的**，例如：

- @Autowired和@Resource有什么区别
- 为什么Spring不建议使用field方式注入
- @Repository、@Componnt、@Controller、@Service有什么区别

总之，硬货有时候就隐藏在很low的问题之下，哈哈哈。

## 参考文档

- [剔除Intellij中Mybatis的Mapper自动注入警告](https://juejin.im/post/5ca4a84e51882510413974fe)
- [idea mybatis 注入 mapper 提示错误](https://www.jianshu.com/p/17be696097ea)

