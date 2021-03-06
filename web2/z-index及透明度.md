# 2.14 z-index及透明度

页面效果：

<img src="https://images.shiguangping.com/imgs/20200720014826.png" alt="image-20200720014826073" width="350px" />

#### `z-index`属性：

z-index 属性指定一个元素的堆叠顺序。

拥有更高堆叠顺序的元素总是会处于堆叠顺序较低的元素的前面。

属性值

| 值       | 描述                                    |
| -------- | --------------------------------------- |
| auto     | 默认。堆叠顺序与父元素相等。            |
| *number* | 设置元素的堆叠顺序。                    |
| inherit  | 规定应该从父元素继承 z-index 属性的值。 |



#### `opacity`属性：

所有主流浏览器都支持opacity属性。.

**注意：**IE8和早期版本支持另一种过滤器属性。像：filter:Alpha(opacity=50)

属性值

| 值      | 描述                                               |
| ------- | -------------------------------------------------- |
| *value* | 指定不透明度。从0.0（完全透明）到1.0（完全不透明） |
| inherit | Opacity属性的值应该从父元素继承                    |



代码：

![image-20200720015157876](https://images.shiguangping.com/imgs/20200720015157.png)