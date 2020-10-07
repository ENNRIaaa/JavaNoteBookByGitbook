# 6.1 FastJson

fastjson是阿里巴巴的开源JSON解析库，它可以解析JSON格式的字符串，支持将Java Bean序列化为JSON字符串，也可以从JSON字符串反序列化到JavaBean。



Java对象序列化成JSON格式字符串：

```java
String text = JSON.toJSONString(obj); //序列化
```



JSON格式字符串反序列化成Java对象：

```java
VO vo = JSON.parseObject("{...}", VO.class); //反序列化
```



JSON对象转成Java对象：

```java
User user = JSON.toJavaObject(jsonObject, User.class);
```



### 代码示例：

定义JavaBean：

```java
public class User {
    private int id;
    private String name;
    private int age;
    private String dateOfBirth;

    public User() {
    }

    public User(int id, String name, int age, String dateOfBirth) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.dateOfBirth = dateOfBirth;
    }
 //此处省略getter/setter方法、toString方法 
}
```



#### JavaBean转换为Json格式字符串

使用`JSON.toJSONString(JavaBean)`方法：

```java
package com.neu.json;

import com.alibaba.fastjson.JSON;
import com.neu.pojo.User;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.util.ArrayList;
import java.util.List;

public class JsonDemo {
    private static ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");

    public static void main(String[] args) {
        User user1 = context.getBean("user1", User.class);
        User user2 = context.getBean("user2", User.class);

        List<User> list = new ArrayList<User>();
        list.add(user1);
        list.add(user2);

        //将Java对象转换为Json格式字符串
        String s = JSON.toJSONString(user1);
        String s1 = JSON.toJSONString(list);
        System.out.println("JavaBean转换为String：" + s);
        System.out.println("封装JavaBean的列表转换为String：" + s1);
    }
}
```

结果：

>JavaBean转换为String：{"age":25,"dateOfBirth":"1995-2-6","id":1001,"name":"张三"}
>封装JavaBean的列表转换为String：[{"age":25,"dateOfBirth":"1995-2-6","id":1001,"name":"张三"},{"age":26,"dateOfBirth":"1994-7-16","id":1002,"name":"李四"}]



#### 将Json格式字符串转为JavaBean

使用`JSON.parseObject(String str, Class<T>)`方法：

```java
//Json格式字符串解析成JavaBean
        String str = "{\"age\":25,\"dateOfBirth\":\"1995-2-6\",\"id\":1004,\"name\":\"小张\"}";
        User user3 = JSON.parseObject(str, User.class);
        System.out.println(user3);
```

结果：

>User{id=1004, name='小张', age=25, dateOfBirth='1995-2-6'}



#### 将JSONObject对象转为JavaBean

使用`JSON.toJavaObject(Json json, Class<T>);`方法：

```java
Map<String, Object> map = new HashMap<String, Object>();
        map.put("id", 1003);
        map.put("name", "小野");
        map.put("age", 27);
        map.put("dateOfBirth", "1993-5-7");
        //JSONObject中有一个带参构造可以传入map
        JSONObject json = new JSONObject(map);

        User user = JSON.toJavaObject(json, User.class);
        System.out.println(user);
```

结果：

> User{id=1003, name='小野', age=27, dateOfBirth='1993-5-7'}





### Servlet中request获取JSON对象

```js
var vm = new Vue({
        el: '#app',
        data: {
            username: '',
            password: '',
        },
        methods: {
            login: function () {
                this.$http.post("./ServletDemo", {
                    username: this.username,
                    password: this.password
                }).then(function (res) {
                    console.log(res.body)
                }, function () {
                    console.log("请求失败")
                })
            }
        }
    })
```

获取前端请求的JSON数据：

```java
//把接收到的request请求数据放到BufferedReader中
        BufferedReader streamReader = new BufferedReader(new InputStreamReader(request.getInputStream(), "UTF-8"));
        //读取缓冲区数据到字符串
        String str = streamReader.readLine();
        //将字符串解析成Json对象
        JSONObject paramsObj  = JSONObject.parseObject(str);
```

得到`paramsObj`之后，就可以像操作Map一样获取JSON中的数据了。