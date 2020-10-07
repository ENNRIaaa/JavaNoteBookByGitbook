# 23.6 得到Class类的几种方式

### Class类

包`java.lang.Class`

对象照镜子后可以得到的信息：某个类的属性、方法、构造器、某个类到底实现了哪些接口。对于每个类而言，JRE都为其保留一个不变的Class类型的对象。一个Class对象包含了特定某个结构(class/interface/enum/annotation/primitive type/void[])的有关信息。

- Class本身也是一个类
- Class对象只能由系统建立对象
- 一个加载的类在JVM中只会有一个Class实例
- 一个Class对象对应的是一个加载导JVM中的一个.class文件
- 每个类的实例都会记得自己是由哪个Class所生成
- 通过Class可以完整地得到一个类中的所有被加载地结构
- Class类是Reflection的根源，针对任何你想动态加载、运行的类，唯有先获得相应地Class对象



#### Class类常用方法：

- static ClassforName(String name) name为全限定类名（包名加类名），返回指定类的Class对象

- Object newInstance()：调用缺省构造函数，返回Class对象地一个实例

  ```java
  Class c1 = Class.forName("com.neu.reflect.User");
  User user = (User) c1.newInstance();//获得User对象
  ```

- getName()：返回此Class对象所表示地实体（类、接口、数组类或void）的名称

- Class getSuperClass()：返回当前Class对象的父类的Class对象

- Class[] getInterfaces()：获取当前Class对象的接口

- ClassLoader getClassLoader()：返回该类的类加载器

- Constructor[] getContructors()：返回一个包含某些Constructor对象的数组

- Method getMethod(String name,Class.. T)：返回一个Method对象，此对象的形参类型为paramType

- Field[] getDeclaredFields()：返回Field对象的一个数组



#### 获取Class类对象

- Class.forName("java.util.String")
- Object.class
- new Object().getClass

```java
Class c1 = Class.forName("com.neu.reflect.User");
Class c2 = User.class;
Class c3 = new User().getClass();
```

c1==c2==c3

这是三种获取Class对象的方式



还有一种特殊的，基本类型的包装类有一个TYPE方法也可以获取Class对象：

```java
Class<Integer> type = Integer.TYPE;
```

***只有包装类才有***



#### 哪些类型有Class对象

- class：外部类，成员（成员内部类、静态内部类），局部内部类，匿名内部类
- interface：接口
- []：数组：数组的类型和维度相同就是同一个Class
- enum：枚举
- annotation：注解@interface
- primitive type：基本数据类型
- void



```java
Class<Object> c1 = Object.class;    //类
Class<Comparable> c2 = Comparable.class;    //接口
Class<String[]> c3 = String[].class;    //数组
Class<ElementType> c4 = ElementType.class;  //枚举
Class<Integer> c5 = int.class;  //基本数据类型
Class<Void> c6 = void.class; //void
Class<Class> c7 = Class.class;  //Class本身也是一个类
```

