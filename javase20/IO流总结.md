# 20.1 IO流总结

### 1. 字符流

#### abstract Reader

- 用于读取字符流的抽象类，子类必须实现的方法只有`read(char[] cbuf,int off,int len)`和`close()`

子类：

- class **BufferedReader**
  - 继承自Reader
  - 从字符输入流中读取文本，缓冲各个字符，从而实现字符、数组和行的高效读取。可以指定缓冲区大小，或者使用默认大小。大多数情况下，默认值就已经足够大了。
  - 构造方法：(没有无参构造器)
    - BufferedReader(Reader in) 创建一个使用默认大小的输入缓冲区的缓冲字符输入流
    - BufferedReader(Reader in,int size) 创建一个使用输入缓冲区的缓冲字符输入流并指定大小
  - 常用方法：
    - read() 读取单个字符
    - read(char[] cbuf,int off,int len) 读取字符进数组
    - readLine() 读取一行文本
    - close() 关闭流释放资源
- class **LineNumberReader**
  - 继承自BufferedReader
  - 跟踪行号的缓冲字符输入流
  - 构造方法和BufferedReader一样，都是传入一个输入流，并可以指定缓冲字符输入流的大小
  - 常用方法：
    - 除了父类的方法之外，额外有两个方法
    - getLineNumber() 得到当前行号
    - setLineNumber(int lineNumber) 设置当前行号
- class **InputStreamReader**
  - 继承自Reader
  - 它是字节流和字符流之间的桥梁，它读取字节并使用指定的charset（编码）解析成字符，通俗的说就是**把字节流读取成字符流按照指定的编码方法**。
  - 构造方法：
    - InputStreamReader(InputStream in) 创建一个InputStreamReader使用平台默认的编码方式读取字节流
    - InputStreamReader(InputSteam in, Charset cs) 给定编码方法读取字节输入流
    - InputStreamReader(InputSteam in, Charset cs)  使用指定的字符集解码器
    - InputStreamReader(InputSteam in, String charsetName) 使用指定的字符集
  - 常用方法：
    - read() 读取单个字符
    - read(char[] cbuf,int off,int len) 读取字符进数组
    - getEncoding() 返回字符编码名称
    - close() 关闭流并释放资源
- class **FileReader**
  - 继承自InputStreamReader
  - 用来读取字符文件的类，该类的构造方法假定默认字符编码和默认字节缓冲区大小都是适当的。要自己指定这些值，可以先在FileInputStream上构造一个InputStreamReader



### 2. 字节流

