# Docker的运行机制

Docker是如何运行的。接下来，将从Docker的引擎与架构两个方面对Docker内部的运行与管理机制进行讲解。

- Docker的引擎
- Docker的架构

---

# Docker的引擎

Docker Engine（Docker引擎）是Docker的核心部分，使用的是客户端-服务器（C/S）架构模式，其主要组成部分如图所示：

![img](https://images.shiguangping.com/imgs/20201013112841.png)

可以看出，Docker Engine 中包含了三个核心组件（docker CLI，REST API和docker daemon），具体说明如下 ：

- **Docker CLI(command line interface）：**表示Docker命令行接口 ，开发者可以在命令行中使用Docker相关执行与Docker守护进程进行交互，从而管理诸如image（镜像）、container（容器）、network（网络）和data volumes（数据卷）等实体。
- **REST API：**表示应用程序API接口，开发者通过该API接口可以与Docker的守护进程进行交互，从而指示后台进行相关操作。
- **docker daemon：**表示Docker的服务端组件，它是Docker架构中运行在后台的一个守护进程，可以接受并处理来自命令行接口（Docker CLI）及API接口（REST API）的指令，然后进行相应的后台操作。

对于开发者而言，既可以使用编写好的脚本文件通过REST API来实现与Docker进行交互，也可以直接使用Docker相关指令，通过命令行接口与Docker进行交互，而其他一些Docker应用则是通过底层API和CLI进行交互。

---

# Docker的架构

Docker使用C/S架构，通过Docker的具体架构，了解Docker的整个运行流程。接下来通过官方的架构图对Docker架构进行详细说明。

> Client 通过接口与Server进程通信实现容器的构建，运行和发布。client和server可以运行在同一台集群，也可以通过跨主机实现远程通信。

![img](https://images.shiguangping.com/imgs/20201013112926.png)

从图上可以看出，Docker架构主要包括Client、DOCKER_HOST和Register三部分，这三部分的具体说明如下：

## **1.Client（客户端）**

Client即Docker客户端，也就是**Docker CLI（**Docker命令行接口**）。**开发者通过和客户端使用Docker的相关指令与 Docker守护进程进行交互，从而进行Docker镜像的创建、拉取和运行等操作。

## **2.DOCKER_HOST(Docker主机)**

DOCKER_HOST即Docker内部引擎运行的主机，主要指Docker daemon(Docker守护进程)。可以通过守护进程与客户端还有Docker的镜像仓库（Registry）进行交互，从而管理Images（镜像）和Containers(容器)等。

## **3.Registry（注册中心）**

Registry即Docker注册中心，实质就是Docker的**镜像仓库，**默认使用的是Docker官方远程注册中心Docker Hub，也可以使用开发者搭建的本地仓库。Registory中包含了大量的镜像，这些镜像可以是官方基础镜像，也可以是其他开发者上传的镜像 。

## **其他**

我们在实际使用Docker时，除了会涉及以上3个主要部分外，还会涉及很多Docker Objects（Docker 对象），例如：Image(镜像)、Containers（容器）、Networks（网络）、Volumes（数据卷）、Plugin（插件）等。其中常见的两个对象Image(镜像)和Containers（容器）。

**Image(镜像)**

Docker镜像就是一个只读模板，包括了一些创建Docker容器的操作指令。通常情况下，一个Docker镜像是基于另一个基础镜像创建的，并且新创建 镜像会额外包含一些功能配置。例如：开发者可以依赖一个Ubuntu的基础镜像创建一个新镜像，并可以在新镜像中安装Apache等软件或其他应用程序。

**Containers（容器）**

Docker容器属于镜像的一个可运行实例（镜像与容器的关系其实与 编程语言中的类与对象相似），开发者可以通过 API接口或者CLI命令接口来 创建、运行、停止、移动、删除一个容器，也可以将一个容器连接到一个或多个网络中，将数据存储与容器进行关联。