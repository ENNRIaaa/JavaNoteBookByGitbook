# 1.1 安装JDK

### 扩展： JDK 科普

**Java Development Kit**（**JDK**）是[太阳微系统](https://zh.wikipedia.org/wiki/昇陽電腦)针对[Java](https://zh.wikipedia.org/wiki/Java)开发人员发布的免费[软件开发工具包](https://zh.wikipedia.org/wiki/软件开发工具包)（SDK，Software development kit）。自从Java推出以来，JDK已经成为使用最广泛的Java SDK。由于JDK的一部分特性采用商业许可证，而非开源[[1\]](https://zh.wikipedia.org/wiki/JDK#cite_note-1)。因此，2006年太阳微系统宣布将发布基于[GPL](https://zh.wikipedia.org/wiki/GPL)的开源JDK，使JDK成为[自由软件](https://zh.wikipedia.org/wiki/自由软件)。在去掉了少量闭源特性之后，太阳微系统最终促成了[GPL](https://zh.wikipedia.org/wiki/GPL)的[OpenJDK](https://zh.wikipedia.org/wiki/OpenJDK)的发布。

作为Java语言的SDK，普通用户并不需要安装JDK来运行Java程序，而只需要安装[JRE](https://zh.wikipedia.org/wiki/JRE)（Java Runtime Environment）。而程序开发者必须安装JDK来编译、调试程序。

#### 包含组件：

JDK包含了一批用于Java开发的组件，其中包括：

- [javac](https://zh.wikipedia.org/wiki/Javac)：[编译器](https://zh.wikipedia.org/wiki/编译器)，将[后缀名](https://zh.wikipedia.org/wiki/后缀名)为.java的[源代码](https://zh.wikipedia.org/wiki/源代码)编译成后缀名为“.class”的[字节码](https://zh.wikipedia.org/wiki/字节码)
- java：运行工具，运行.class的字节码
- [jar](https://zh.wikipedia.org/w/index.php?title=Jar&action=edit&redlink=1)：打包工具，将相关的类文件打包成一个文件
- [javadoc](https://zh.wikipedia.org/wiki/Javadoc)：[文档](https://zh.wikipedia.org/wiki/文档)生成器，从源码[注释](https://zh.wikipedia.org/wiki/注释)中提取文档，注释需符合规范
- jdb debugger：[调试工具](https://zh.wikipedia.org/wiki/调试工具)
- jps：显示当前java程序运行的[进程](https://zh.wikipedia.org/wiki/进程)状态
- javap：[反编译](https://zh.wikipedia.org/wiki/反編譯器)程序
- appletviewer：运行和调试[applet](https://zh.wikipedia.org/wiki/Applet)程序的工具，不需要使用[浏览器](https://zh.wikipedia.org/wiki/浏览器)
- javah：从Java类生成C[头文件](https://zh.wikipedia.org/wiki/头文件)和C源文件。这些文件提供了连接胶合，使Java和C代码可进行交互。[[2\]](https://zh.wikipedia.org/wiki/JDK#cite_note-2)
- javaws：运行[JNLP](https://zh.wikipedia.org/w/index.php?title=JNLP&action=edit&redlink=1)程序
- extcheck：一个检测jar包冲突的工具
- apt：注释处理工具[[3\]](https://zh.wikipedia.org/wiki/JDK#cite_note-3)
- jhat：java[堆](https://zh.wikipedia.org/wiki/堆)分析工具
- jstack：[栈](https://zh.wikipedia.org/wiki/栈)跟踪程序
- jstat：[JVM](https://zh.wikipedia.org/wiki/JVM)检测统计工具
- jstatd：jstat[守护进程](https://zh.wikipedia.org/wiki/守护进程)
- jinfo：获取正在运行或崩溃的java程序配置信息
- jmap：获取java进程内存映射信息
- idlj：[IDL](https://zh.wikipedia.org/wiki/IDL)-to-Java编译器。将[IDL](https://zh.wikipedia.org/wiki/IDL)语言转化为java文件[[4\]](https://zh.wikipedia.org/wiki/JDK#cite_note-4)
- policytool：一个[GUI](https://zh.wikipedia.org/wiki/GUI)的[策略文件](https://zh.wikipedia.org/w/index.php?title=策略文件&action=edit&redlink=1)创建和管理工具
- jrunscript：[命令行](https://zh.wikipedia.org/wiki/命令行)[脚本](https://zh.wikipedia.org/wiki/脚本)运行

JDK中还包括完整的JRE（Java Runtime Environment），Java运行环境，也被称为*private* runtime。包括了用于产品环境的各种库类，如基础类库rt.jar，以及给开发人员使用的补充库，如[国际化与本地化](https://zh.wikipedia.org/wiki/国际化与本地化)的[类库](https://zh.wikipedia.org/wiki/类库)、[IDL](https://zh.wikipedia.org/wiki/IDL)库等等。

JDK中还包括各种[样例程序](https://zh.wikipedia.org/w/index.php?title=样例程序&action=edit&redlink=1)，用以展示[Java API](https://zh.wikipedia.org/w/index.php?title=Java_API&action=edit&redlink=1)中的各部分。



### JRE

**Java运行环境**（Java Runtime Environment，简称JRE）是一个软件，由太阳微系统所研发，JRE可以让[电脑系统](https://zh.wikipedia.org/wiki/電腦系統)运行Java应用程序（Java Application）。

JRE的内部有一个Java虚拟机（Java Virtual Machine，[JVM](https://zh.wikipedia.org/wiki/JVM)）以及一些标准的[类别](https://zh.wikipedia.org/wiki/類別)[函数库](https://zh.wikipedia.org/wiki/库)（Class Library）。

---



*来页面的介绍大都来自[维基百科](https://zh.wikipedia.org/wiki/JDK)。*





