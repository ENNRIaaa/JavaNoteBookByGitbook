# Jenkins 介绍与搭建

Jenkins 是一款流行的开源的持续集成 (CI) 工具，广泛用于项目开发，具有自动化构建、测试和部署等功能。

Jenkins 的特征：

- 开源的Java语言开发持续集成工具，支持持续集成，持续部署。
- 易于安装部署，可通过yum安装，或者通过docker容器等快速安装部署。
- 消息通知及测试报告：集成RSS/E-mail通过RSS发布构建结果或当构建完成时通过e-mail通知，生成Junit/TestNG测试报告。
- 分布式构建：支持Jenkins能够让多台计算机一起构建、测试。
- 文件识别：Jenkins能够跟踪哪次构建生成哪些jar，哪次构建使用哪个版本的jar等
- 丰富的插件支持

### 搭建Gitlab代码仓库

-- 待写 --



### 搭建Jenkins持续集成环境

[Docker安装Jenkins](https://www.shiguangping.com/2020/09/docker-install-jenkins)

*当前笔记使用的Jenkins版本：Jenkins2.249.2*