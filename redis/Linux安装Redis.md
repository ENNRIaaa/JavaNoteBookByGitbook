# Linux下安装Redis

1. 在[官网](https://redis.io/)下载最新的安装包：redis-6.0.6.tar.gz

2. 通过ftp工具将安装包上传到Linux服务器，之后将安装包放到/opt目录下并解压：

![image-20200812110255616](https://images.shiguangping.com/imgs/20200812110255.png)

3. 进入/redis-6.0.6目录

4. 基本的环境安装：

   ```bash
   yum install gcc-c++
   ```

   gcc安装完毕之后，使用make命令：

   ```bash
   make
   ```

   等待make完毕

5. redis的默认安装目录：

   ```
   /usr/local/bin
   ```

6. 将redis配置文件

   可以在当前`/usr/local/bin`目录下创建目录`rconfig`，目录名自定义。接着将/opt目录下redis中的配置文件拷贝过来：

   ```bash
   cp /opt/redis-6.0.6/redis.conf rconfig/
   ```

   ![image-20200812111601859](https://images.shiguangping.com/imgs/20200812111601.png)

7. Redis默认不是后台启动的，修改配置文件：

   ![image-20200812111706681](https://images.shiguangping.com/imgs/20200812111706.png)

8. 启动Redis服务：

   通过指定的配置文件启动服务：

   ![image-20200812111834667](https://images.shiguangping.com/imgs/20200812111834.png)

9. 使用redis-cli进行连接测试：

   ![image-20200812122020425](https://images.shiguangping.com/imgs/20200812122020.png)

   10. 查看redis的进程是否开启：

       ```bash
        ps -ef|grep redis
       ```

       ![image-20200812122803923](https://images.shiguangping.com/imgs/20200812122803.png)

   11. 关闭Redis服务：(进入到redis-cli中，shutdown)

       ![image-20200812123628821](https://images.shiguangping.com/imgs/20200812123628.png)

   12. 

   

   

   

