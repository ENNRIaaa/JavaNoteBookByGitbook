# 4.7 Vue部分--查

查询这里我做了分页查询，样式使用的`element-ui`的分页组件，后端sql通过limit分页查询，又额外添加了一个返回数据库总条目数的查询方法。

#### 前端的分页组件：

1. 在`components`中创建`QueryUserAll.vue`
2. 先上代码，之后再详细说明分页的实现：

![image-20200705233740907](https://images.shiguangping.com/imgs/20200705233740.png)

```vue
<el-pagination
               @current-change="handleCurrentChange"
               background
               layout="prev, pager, next"
               :pager-count="5"
               :page-size="pageSize"
               :total="total"
               :current-page="currentPage">
</el-pagination>
```

这个是`element-ui`的分页组件：

- `@current-change`：当前页发生改变时，调用`handleCurrentChange`方法：

  ```javascript
  handleCurrentChange(val) {
    //当前页发生改变时，将当前页码赋值给this.currentPage属性
    this.currentPage=val
    //并调用查询方法，查询改变后当前页码的数据
    this.queryUserAll()
  }
  ```

- `background`：分页样式有背景

- `layout`：上一页、页码、下一页

- `:pager-count="5"`：页码超过指定值时自动折叠

- `:page-size="pageSize"`：每页显示数据的条目数

- `:total="total"`：总条目数

- `:current-page="currentPage"`：当前页码

最后三个参数是比较重要的，涉及到后端查询的，

MySql中，limit查询需要提供两个参数(index,size)，查询的起始位置，查询的条目数

- 起始位置对应：this.currentPage - 1 将当前页码-1传递给后端即可（limit查询起始位置从0开始，而分页的页码是从1开始）
- 查询的条目数对应：this.pageSize  （即每页显示的条目数，前端需要每页显示多少条数据，直接将条目数传递给后端即可）
- 还有一个就是后端需要返回给当前数据库中总的条目数，只需要查询count，返回总数目即可，这个对应分页组件的`:total="total"`总条目数

有了这三个关键的参数，就可以实现分页查询。



#### 分页查询的作用：

当查询数据，要返回的数据量比较大时，会对前端造成比较大的压力，可能会影响用户体验。如果同时访问人数比较多，对数据库服务器的性能以及带宽都会有影响。

分页查询的主要目的就是能够缓解对前端的压力以及对数据库查询的压力，一次性返回过多的数据对内存，对带宽都是不小的冲击。



#### Step2：`index.js`添加路由

![image-20200706001202603](https://images.shiguangping.com/imgs/20200706001202.png)

#### Step3：`App.vue`添加链接

![image-20200706001244819](https://images.shiguangping.com/imgs/20200706001244.png)



#### 分页查询的效果：

![image-20200706001316960](https://images.shiguangping.com/imgs/20200706001317.png)

![image-20200706001334386](https://images.shiguangping.com/imgs/20200706001334.png)

下面的页码也会随着数据的增加而增加、减少而减少，通过后端返回的数据表总条目数以及每页显示的条数，动态的分页。



**至此，SSM整合，从零搭建就结束了**



*刚刚跟着视频学完Spring的时候，对控制反转以及依赖注入不是很理解。写代码的方式上，也不习惯。之前一直都是敲Java代码，现在变成了写配置文件。*

*紧接着学完Mybatis，通过Spring整合Mybatis，由Spring去管理Mybatis，整合的时候更懵了。*

*但是，随着不断的向后学习，学完SpringMVC，跟着视频整合SSM之后，真正完成了一个简单的项目，简单的增删改查功能之后，我对这几个框架之间的关系，每个框架的作用有了新的认识。*

*从第一遍第二遍照着笔记搭建，到后来慢慢理解每一步的作用，能独立搭建SSM，这是对于一个初学者来说，最兴奋的事儿了。*

*更兴奋的是，理解了之后，对于注解的使用更加上手，虽然就那么几个注解，但是不理解Spring的话，用注解总是有种懵懂的感觉--。*

*学习编程的体会：*

- *学习新技术的时候，跟着视频敲代码，一定要记笔记，这个是把知识转化的一个过程。光看视频是看不会的，要是看就能看会，那他肯定是个天才。*
- *记笔记可以让思路更清晰，笔记是出自自己之手，而不是像在网上看别人写的文章一样，看得一脸懵逼。当之后遇到不理解的问题时翻看自己的笔记，更容易吸收。*
- *学习的时候，遇到实在不理解的地方不要花时间去纠结，继续往下看，等把一个技术拿下之后就会发现之前不理解的地方现在已经想通了。*

