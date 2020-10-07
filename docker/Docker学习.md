# Docker学习

Docker是基于Go语言开发的

官方文档：https://docs.docker.com/

Docker Hub：https://hub.docker.com/

Docker 是一个开源工具，它可以让创建和管理 Linux 容器变得简单。容器就像是轻量级的虚拟机，并且可以以毫秒级的速度来启动或停止。Docker 帮助系统管理员和程序员在容器中开发应用程序，并且可以扩展到成千上万的节点。

![Living in a Docker world - The Verge](https://images.shiguangping.com/imgs/20200710165952.png)

这是一只鲸鱼，它托着许多集装箱。我们可以把宿主机可当做这只鲸鱼，把相互隔离的容器可看成集装箱，每个集装箱中都包含自己的应用程序。



### Docker与传统虚拟区别

传统虚拟化技术的体系架构：

![2](https://images.shiguangping.com/imgs/20200710170132.png)

Docker技术的体系架构：

![3](https://images.shiguangping.com/imgs/20200710170147.png)

容器和 VM（虚拟机）的主要区别是:

- 容器提供了基于进程的隔离，而虚拟机提供了资源的完全隔离。
- 虚拟机可能需要一分钟来启动，而容器只需要一秒钟或更短。
- 容器使用宿主操作系统的内核，而虚拟机使用独立的内核。