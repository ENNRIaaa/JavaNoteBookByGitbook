# 14.6 Java 多线程

### 线程的概念：

- 进程是指可执行程序并存放在计算机存储器的一个指令序列，它是一个动态执行的过程。
- 线程是比进程还要小的运行单位，一个进程包含多个线程。
- 线程相当于一个子程序。
- CPU使用时间片轮转的工作方式，可以让多个程序轮流占用CPU，达到同时运行的效果



### 线程的创建：

- 创建一个**Thread**类，或者一个Thread子类的对象
- 创建一个实现**Runnable**接口的类的对象



### Thread类

- Thread是一个线程类，位于java.lang包下

```java
//构造方法：
Thread();	//创建一个线程对象
Thread(String name);	//创建一个具有指定名称的线程对象
Thread(Runnable target);	//创建一个基于Runnable接口实现类的线程对象
Thread(Runnable target,String name) ;	//创建一个基于Runnable接口实现类，并且具有指定名称的线程对象
```

```java
//常用方法：
public void run(); //线程相关的代码写在该方法中，一般需要重写
public void start(); //启动线程的方法
public static void sleep(long m); //线程休眠m毫秒的方法
public void join();	//优先执行调用join()方法的线程
```



### Runnable接口

- 只有一个方法 run();
- Runnable是Java中用以实现线程的接口
- 任何实现线程功能的类都必须实现该接口