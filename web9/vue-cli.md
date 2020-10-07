# vue-cli脚手架

### 什么是CLI ？

命令行界面(command-line interface)，缩写成CLI，是在图形用户界面得到普及之前使用最为广泛的用户界面，它通常不支持鼠标，用户通过键盘输入指令，计算机接收到指令之后，予以执行。也有人称其为字符用户界面CUI



### 什么是Vue-CLI ？

Vue CLI是一个机遇Vue.js进行快速开发的完整系统。使用Vue脚手架之后，我们开发的页面将是一个完整的系统（项目），而不是单单的页面了。



- 通过 `@vue/cli` 实现的交互式的项目脚手架。之前需要使用bootstrap JQuery等都需要下载引入这些库，而现在只需要通过命令就可以下载相关依赖
- 通过 `@vue/cli` + `@vue/cli-service-global` 实现的零配置原型开发。
- 一个运行时依赖 (@vue/cli-service)，该依赖：
  - 可升级；
  - 基于 webpack 构建，并带有合理的默认配置；webpack：项目打包工具，编译好的项目源码===》部署到服务器上
  - 可以通过项目内的配置文件进行配置；
  - 可以通过插件进行扩展。
- 一个丰富的官方插件集合，集成了前端生态中最好的工具。
- 一套完全图形化的创建和管理 Vue.js 项目的用户界面。



### 安装Vue-Cli

安装Vue-Cli：

```bash
npm install -g @vue/cli
```

查看版本：

```bash
vue --version
```





### 创建Vue项目

进入到要创建项目的目录，通过`vue create`创建项目（项目名使用中划线或者下划线连接）,然后根据提示选择配置进行创建Vue项目:

```bash
vue create projectname
```



终端指令：图形化快速创建构建项目：

```
vue ui
```



或者，通过webstorm等IDE构建vue项目



### 通过npm运行项目

终端进入项目目录，通过`npm run serve`命令运行项目

Windows 平台命令：`npm run dev`

