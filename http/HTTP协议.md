# HTTP协议

## Http简介

HTTP（超文本传输协议）是一个机遇请求和响应模式的、无状态的、应用层的协议。

![image-20201014220908118](https://images.shiguangping.com/imgs/20201014220908.png)



## URL介绍

百度搜索的一个URL地址：

```
https://www.baidu.com/s?wd=%E4%B8%8A%E6%B5%B7%E6%82%A0%E6%82%A0%E5%8D%9A%E5%AE%A2&rsv_spt=1&rsv_iqid=0x91baaabd00070ba2&issp=1&f=8&rsv_bp=1&rsv_idx=2
```

- http/https：协议类型
- host：主机地址或域名
  - 192.168.x.xx:8080 地址+端口号
  - Localhost:8080 localhost是本机地址（127.0.0.1）
- port：端口号（http默认端口号80，https默认端口号443）
- path：请求的路径（host之后，问号?之前）
- 参数：name=value
- &：多个参数用&隔开



## Get/Post请求

Get请求如下图：

![image-20201014221326390](https://images.shiguangping.com/imgs/20201014221326.png)

Get请求没有请求体，它的请求参数拼接在URL上。



![image-20201014221411140](https://images.shiguangping.com/imgs/20201014221411.png)

Post请求有请求体，请求参数在请求体中。请求体也可以为空。



**请求方法：**

根据HTTP标准，HTTP请求可以使用多种请求方法。

HTTP1.0定义了三种请求方法：Get、Post、Head

HTTP1.1新增了五种请求方法：OPTIONS、PUT、DELETE、TRACE、CONNECT



## Request组成

客户端发送一个Http请求到服务器的请求消息包括以下格式：

请求行(request line)、请求头(header)、请求空行、请求数据（请求体）四个部分组成、

![image-20201014221836968](https://images.shiguangping.com/imgs/20201014221837.png)



### 请求头 header

![image-20201014221915185](https://images.shiguangping.com/imgs/20201014221915.png)

Client：

- Accept：浏览器可接受的媒体类型
- Accept-Language：语言
- Accept-Encoding：编码格式
- User-Agent：客户端类型

Cookie：身份认证（一种会话技术）

Entity：

- Content-Type：发送post时候，body的数据类型声明



## Post的请求体

Post请求体的常见数据类型有5种：

- application/json：`{"key1":"xxx","key2":"yyy"}`
- application/x-www-form-urlencoded：`key1=xxx&key2=yyy`
- multipart/form-data：这是一种表单格式
- text/xml
- Content-Type: octets/stream 文件下载的时候



请求体为Json格式：

![image-20201014222732637](https://images.shiguangping.com/imgs/20201014222732.png)



Content-Type: multipart/form-data; 表单类型一般出现在文件上传（不是文件上传也可以）

![image-20201014222819565](https://images.shiguangping.com/imgs/20201014222819.png)



![image-20201014222831124](https://images.shiguangping.com/imgs/20201014222831.png)



## Response

一般情况下，服务器接收并处理客户端发过来的请求后会返回一个HTTP的响应消息。

Http响应也有四个部分组成，分别是：状态行、消息报头、空行、响应正文（响应体）



**状态码：**

状态码有三位数字组成，第一个数字定义了响应的类别，共分五种类别：

- 1xx：指示信息--表示请求已接收，继续处理
- 2xx：成功--表示请求已被陈宫接收、理解、接受
- 3xx：重定向--要完成请求必须进行更进一步的操作
- 301：永久重定向
- 302：临时重定向
- 304：用到缓存，请求服务端资源未改变，用本地未过期缓存
- 4xx：客户端错误--请求有语法错误或请求无法实现
- 5xx：服务器端错误--服务器未能实现合法的请求



**常见状态码：**

200 OK ：客户端请求成功

400 Bad Request ： 客户端请求有语法错误，不能被服务器所理解（一般为请求参数不是后端接口想要的，传参传错了）。

401 Unauthorized ：请求未经授权，这个状态码必须和WWW-Authenticate报头域一起使用

403 Forbidden ： 服务器收到请求，但是拒绝提供服务

404 Not Found ： 请求资源不存在，可能输入了错误的Url

500 Internal Server Error ： 服务器发生了不可预期的错误（一般是后端代码运行时报错，检查后端代码）

503 Server Unavailable ： 服务器当前不能处理客户的请求，一段时间后可能恢复正常