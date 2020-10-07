# 5.10 thymeleaf模板引擎

引入Maven依赖：

```xml
<dependency>
  <groupId>org.thymeleaf</groupId>
  <artifactId>thymeleaf-spring5</artifactId>
</dependency>
<dependency>
  <groupId>org.thymeleaf.extras</groupId>
  <artifactId>thymeleaf-extras-java8time</artifactId>
</dependency>
```



Thymeleaf 的属性配置类：

```java
@ConfigurationProperties(prefix = "spring.thymeleaf")
public class ThymeleafProperties {

	private static final Charset DEFAULT_ENCODING = StandardCharsets.UTF_8;

	public static final String DEFAULT_PREFIX = "classpath:/templates/";

	public static final String DEFAULT_SUFFIX = ".html";
```

Thymeleaf模板引擎默认的前缀是`classpath:/templates/`，默认的后缀是：`.html`

所以，写一个控制类：

```java
@Controller
public class IndexController {
    @RequestMapping("/test")
    public String index(){
        return "test";
    }
}
```

直接访问`http://localhost:8081/test`，就可以访问到`resources/templates/test.html`。

配置类`prefix = "spring.thymeleaf"`，我们可以通过配置文件来修改Thymeleaf模板引擎的前缀和后缀。



#### 表达式：

- 简单表达：
- 变量表达式：`${...}`
- 选择变量表达式：`*{...}`
- 消息表达式：`#{...}`
- 链接网址表达式：`@{...}`
- 片段表达式：`~{...}`
- Literals
- 文字 literals：`'one text'`，`'Another one!'`，...
- 数字 literals：`0`，`34`，`3.0`，`12.3`，...
- Boolean literals：`true`，`false`
- 空文字：`null`
- 文字代币：`one`，`sometext`，`main`，......
- 文字操作：
- String 连接：`+`
- 字面替换：`|The name is ${name}|`
- 算术运算：
- 二进制 operators：`+`，`-`，`*`，`/`，`%`
- 减号(一元运算符)：`-`
- Boolean 操作：
- 二进制操作符：`and`，`or`
- Boolean negation(一元 operator)：`!`，`not`
- 比较和平等：
- 比较器：`>`，`<`，`>=`，`<=`(`gt`，`lt`，`ge`，`le`)
- Equality operators：`==`，`!=`(`eq`，`ne`)
- 有条件的 operators：
- If-then：`(if) ? (then)`
- If-then-else：`(if) ? (then) : (else)`
- 默认值：`(value) ?: (defaultvalue)`
- 特殊代币：
- No-Operation：`_`





| 订购 | 特征                | 属性                                       |
| :--- | :------------------ | :----------------------------------------- |
| 1    | 片段包含            | `th:insert` `th:replace`                   |
| 2    | 片段迭代            | `th:each`                                  |
| 3    | 有条件的 evaluation | `th:if` `th:unless` `th:switch` `th:case`  |
| 4    | 局部变量定义        | `th:object` `th:with`                      |
| 5    | 一般属性修改        | `th:attr` `th:attrprepend` `th:attrappend` |
| 6    | 具体属性修改        | `th:value` `th:href` `th:src` `...`        |
| 7    | 文字(标签正文修改)  | `th:text` `th:utext`                       |
| 8    | 片段规范            | `th:fragment`                              |
| 9    | 片段删除            | `th:remove`                                |

