# Pipeline流水线项目构建

#### Pipeline介绍

Pipeline，简单来说，就是一套运行在Jenkins上的工作流框架，将原来独立运行于单个或者多个节点的任务连接起来，实现单个任务难以完成的复杂流程编排和可视化的工作。

#### 如何创建Jenkins Pipeline？

- Pipeline脚本是由Groovy语言实现的
- Pipeline支持两种语法：Declarative（声明式）和Scripted Pipeline（脚本式）语法
- Pipeline有两种创建方法：可以直接在Jenkins的WebUI界面中输入脚本；也可以创建一个Jenkinsfile脚本文件放入项目源码库中（一般使用后面的方法）。

#### 创建流水线项目

如果Jenkins没有安装Pipeline插件，需要到插件管理安装Pipeline相关的插件。

新建流水线任务：

![image-20201101211803929](https://images.shiguangping.com//imgs/20201101211803.png)

流水线脚本演示：

示例代码（声明式）：

```groovy
pipeline {
    agent any

    stages {
        stage('pull code') {
            steps {
                echo 'pull code'
            }
        }
        stage('build project') {
            steps {
                echo 'build project'
            }
        }
        stage('publish project') {
            steps{
                echo 'publish project'
            }
        }
    }
}
```

- agent 代理
- stages 阶段
- stage 每个阶段
- steps 步骤



控制台打印构建信息：

![image-20201101213012214](https://images.shiguangping.com//imgs/20201101213012.png)

示例代码（脚本式）：

```groovy
node {
    def mvnHome
    stage('pull code') { // for display purposes
        echo 'pull code'
    }
    stage('build project') {
        echo 'build project'
    }
    stage('publish project') {
        echo 'publish project'
    }
}
```

