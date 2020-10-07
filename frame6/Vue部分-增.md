# 4.4 Vue部分--增

使用IDE打开刚刚创建好的Vue项目，把预带的不需要的组件都删除掉，之后开始写第一个页面功能，“注册用户”，`增加User`。



开始写增加User功能（注册功能）之前，突然想到一个问题，数据表中username字段设置了unique(唯一约束)，username不能重复，如果注册时输入了已有的用户名，Java程序会报错。

所以，先修改一下后端代码，在Dao层接口中添加一个方法，用来校验是否有重复用户名：

![image-20200627174429109](https://images.shiguangping.com/imgs/20200627174429.png)

修改了接口，紧接着就要修改Usermapper.xml，添加查询语句：

![image-20200627174513123](https://images.shiguangping.com/imgs/20200627174513.png)

service层接口和实现类也要做修改：

![image-20200627174602201](https://images.shiguangping.com/imgs/20200627174602.png)

service层实现类：

*在实现类`addUser()`方法中做用户名是否重复的验证*

![image-20200627175036163](https://images.shiguangping.com/imgs/20200627175036.png)



#### 后端修改完毕，回到前端IDE，开始写Vue代码：

在`components`目录下新建`AddUser.vue`文件：

![image-20200627175545640](https://images.shiguangping.com/imgs/20200627175545.png)

在`template`标签中添加两个输入框、一个按钮，我这里输入框使用的是`element-ui`组件库，这个可以自己研究一下。

方法中使用axios作为异步通信，安装axios库后，需要在`main.js`中导入组件，并添加到原型中，我把它放到下面的图中了：⬇️⬇️



在`router`目录下，新建`index.js`文件：

![image-20200627180208563](https://images.shiguangping.com/imgs/20200627180208.png)



编写`main.js`：

![image-20200627180703448](https://images.shiguangping.com/imgs/20200627180703.png)

编写`App.vue`：

![image-20200627181030005](https://images.shiguangping.com/imgs/20200627181030.png)



运行效果：

用户名重复时：

![image-20200627181315495](https://images.shiguangping.com/imgs/20200627181315.png)

注册成功时：

![image-20200627181512430](https://images.shiguangping.com/imgs/20200627181512.png)



***注册功能（增）写完了~***



饿了吗UI组件库的官方使用文档：https://element.eleme.cn/#/zh-CN/component/