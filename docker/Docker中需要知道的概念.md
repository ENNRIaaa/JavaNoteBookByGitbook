# Docker中需要知道的概念

#### Docler的基本组成：

![img](https://images.shiguangping.com/imgs/20200710204658.PNG)

- Client：客户端
- Docker_Host：主机，服务器
- Registry：仓库



- 镜像（images）：

  docker镜像就好比一个模板，可以通过这个模板来创建容器服务。

  就像图中的镜像一样，可以通过镜像创建多个容器，各自运行

- 容器（Containers）：

  Docker利用容器技术，独立运行一个或者一组应用，通过镜像来创建的。

  容器的基本命令：启动、停止、删除等

- 仓库（Repository）：

  仓库是用来存放镜像的地方，仓库分公有仓库和私有仓库。