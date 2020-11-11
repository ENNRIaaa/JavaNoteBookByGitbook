# Fiddler的工作原理

## Fiddler配置

Fiddler是一个比较常用的抓包工具。

当终端设备（web、app）发出请求，fiddler作为代理，传给服务器；服务器返回数据，fiddler再拦截，而后传给终端设备。

![img](https://images.shiguangping.com/imgs/20201014203211)



Fiddler下载地址：[https://www.telerik.com/download/fiddler-everywhere](https://www.telerik.com/download/fiddler-everywhere)



### 抓取手机请求

如果需要抓手机，则手机连接的WiFi要与Fiddler所在主机（电脑）在通一个局域网，并且将WIFI中的HTTP代理的IP地址设置为Fiddler主机的IP地址，端口设置为Fiddler中的端口（如下图的8866）。

<img src="https://images.shiguangping.com/imgs/20201014205622.png" alt="image-20201014205622846" style="width: 600px" />

这些设置好之后，Fiddler就可以抓取手机了，默认抓取HTTP请求。如果要抓取HTTPS请求，需要先通过手机访问Fiddler主机IP＋端口号（如：192.168.3.2:8866），会访问到Fiddler服务的一个页面，点击最下面的下载root证书，安装好证书之后，Fiddler就可以正常抓取手机的HTTPS请求。