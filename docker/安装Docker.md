# 安装Docker

我当前的Linux环境是Cent OS8

#### 安装步骤：

1 卸载旧的版本

```shell
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```



2 安装`yum-utild`包：

```shell
sudo yum install -y yum-utils
```



3 添加镜像仓库：

```shell
sudo yum-config-manager \
--add-repo \
https://download.docker.com/linux/centos/docker-ce.repo

# 或者添加阿里的镜像仓库
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```



更新软件包索引：

```shell
sudo yum makecache fast
```



5 安装Docker引擎 社区版：

- docker-cd 社区版
- decker-ee 企业版

```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```



6 启动Docker：

```shell
sudo systemctl start docker
```



使用`docker version`命令查看版本：

```shell
docker version
```

<img src="https://images.shiguangping.com/imgs/20200709234150.png" alt="image-20200709234150301" width="600px"/>



7 运行Hello World

```shell
sudo docker run hello-world
```

<img src="https://images.shiguangping.com/imgs/20200709234718.png" alt="image-20200709234718335" width="600px" />



查看拉取下来的`hello-world`镜像：

```bash
docker images
```

查看所有镜像



卸载Docker：

Uninstall the Docker Engine, CLI, and Containerd packages:

```bash
sudo yum remove docker-ce docker-ce-cli containerd.io
```



Images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes:

```bash
sudo rm -rf /var/lib/docker
```



## Docker的启动与停止

systemctl 命令是系统服务管理器指令 

启动docker：

```
systemctl start docker
```



停止docker：

```
systemctl stop docker
```



重启docker：

```
systemctl restart docker
```



查看docker状态：

```
systemctl status docker
```



开机启动：

```
systemctl enable docker
```



查看docker概要信息

```
docker info
```



查看docker帮助文档

```
docker --help
```



