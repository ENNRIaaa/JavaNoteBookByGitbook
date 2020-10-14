# Docker的底层技术

> 简单说明。

Docker使用了一系列的底层技术来充分发挥其技术特色，这些底层技术包括Namespaces、Control groups、Union file systems 和 Container format等，其具体含义如下：

## 1.Namespaces （名称空间）

Docker使用名称空间来为容器提供隔离的工作空间。当一个容器运行时，Docker就会为该容器创建一系列的名称空间，并且名称空间提供一层隔离。当一个容器都运行在相对隔离的环境下，对其他名称空间是相对受限的。

## 2.Control groups（控制组）

基于Linux系统的Docker引擎也依赖另一项叫Control groups（cgroups，控制组）的技术。控制组可以对程序进行资源限定，并允许Docker引擎在容器间进行硬件资源共享以及随时进行限制和约束，例如：开发者可以限制某种特定容器 可用内存。

## 3.Union file systems （联合文件系统）

联合文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统，它支持将文件系统的修改作为一次提交来一层层地叠加，同时可以将不同的目录挂载到同一个虚拟文件系统下。不同Docker容器可以共享一些基础的文件系统层，与自己独有的改动层一起使用，可以大大提高存储效率。Docker目前支持的联合文件系统包括AUFS、btrfs、vfs和DeviceMapper。

## 4.Container format （容器格式）

Docker引擎将命名空间、控制组和联合文件系统组合成一个叫容器格式的整体。当前默认的容器格式是libcontainer，未来Docker可能ui通过与其他技术（如BSD Jails 或者 Solaris Zones）的集成使用来开发其他的容器格式。