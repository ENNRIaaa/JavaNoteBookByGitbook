# IDEA配置Maven

*小贴士：我用的IDEA安装了中文汉化插件（官方的），在首选项中 ->Plugin中搜索"chinese"进行安装：*

<img src="https://images.shiguangping.com/imgs/20200628165104.png" alt="image-20200628165104901" style="zoom:33%;" />



### IDEA配置Maven：

在欢迎界面，右下角 配置 -> 首选项

*（这里面配置的，是对新项目配置的都有效，通俗的说，就是全局的）*

![image-20200628164102657](https://images.shiguangping.com/imgs/20200628164102.png)

构建、执行、部署 -> 构建工具 -> Maven：

![image-20200628164636577](https://images.shiguangping.com/imgs/20200628164636.png)



***确定之后，IDEA的Maven已经配置结束了，每次我们在创建新项目的时候，都会引用我们配置好的Maven来构建新项目***



### IDEA构建普通Maven项目（不使用骨架）：

![image-20200628175910400](https://images.shiguangping.com/imgs/20200628175910.png)

或者，在IDEA内通过 `文件 -> 新建 ->项目`创建项目。



创建新项目：选择Maven：

![image-20200628180054926](https://images.shiguangping.com/imgs/20200628180054.png)

下一步：

![image-20200628180557622](https://images.shiguangping.com/imgs/20200628180557.png)

然后，点击完成。

一个Maven项目构建完毕：

![image-20200628180634800](https://images.shiguangping.com/imgs/20200628180634.png)

这只是一个普通的Maven项目，**如果要添加Web支持：**

![image-20200628180807494](https://images.shiguangping.com/imgs/20200628180807.png)

项目名右键 -> 添加框架支持：勾选`Web Application`：

![image-20200628180941601](https://images.shiguangping.com/imgs/20200628180941.png)

此时，项目已经变成了Web项目了：

<img src="https://images.shiguangping.com/imgs/20200628181013.png" alt="image-20200628181013028" style="zoom:50%;" />

注意观察web目录文件夹图标有一个小蓝点，这说明目录有效。如果因为某些原因，web目录图标没有小蓝点，那可能是项目构建的过程中出现了问题。



### 通过骨架直接构建Web项目：

只需要在新建项目这一步，选中`通过原型创建`，选择下面的红框中的原型即可：

![image-20200628181701061](https://images.shiguangping.com/imgs/20200628181701.png)

