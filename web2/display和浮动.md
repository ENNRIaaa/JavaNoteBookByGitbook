# 2.9 display和浮动

本节内容：

- display属性
- float属性：浮动
- 父级元素塌陷解决
- overflow属性

---

#### `display`属性：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
      /*
      display属性值：
      block：块（可以把行内元素变成展示成块元素）
      inline：行内元素（可以把块元素展示成行内元素）
      inline-block：行内块元素
      none：不展示
      */
      div{
        width: 100px;
        height: 100px;
        border: 1px black solid;
        display: inline-block;
      }

      span{
        width: 100px;
        height: 100px;
        border: 1px black solid;
        display: inline-block;
      }
    </style>
  </head>
  <body>
    <div>div块元素</div>
    <span>span行内元素</span>
  </body>
</html>

```

display属性值：

- block：块（可以把行内元素变成展示成块元素）
- inline：行内元素（可以把块元素展示成行内元素）
- inline-block：行内块元素
- none：不展示



#### 浮动`float`：

CSS 的 Float（浮动），会使元素向左或向右移动，由于浮动的元素会脱离文档流，所以其周围的元素也会重新排列。

元素的水平方向浮动，意味着元素只能左右移动而不能上下移动。

一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。

浮动元素之后的元素将围绕它。

浮动元素之前的元素将不会受到影响。



#### 清除浮动 - 使用 `clear`：

元素浮动之后，周围的元素会重新排列，为了避免这种情况，使用 clear 属性。

clear 属性指定元素两侧不能出现浮动元素。



| 属性  | 描述                               | 值                               | CSS  |
| ----- | ---------------------------------- | -------------------------------- | ---- |
| clear | 指定不允许元素周围有浮动元素。     | left  right  both  none  inherit | 1    |
| float | 指定一个盒子（元素）是否可以浮动。 | left  right  none  inherit       | 1    |

*CSS1指在css1版本中定义的属性。*



#### 父级边框塌陷问题

父级塌陷：父元素的高度是由内部子元素撑起来的，当内部的子元素浮动之后会脱离文档流，所以父元素的高度会塌陷。如果内部的子元素都浮动起来的话，父元素就会如下图一样，只剩下本身内边距的高度。

![image-20200719201148307](https://images.shiguangping.com/imgs/20200719201148.png)

解决方案：

- 增加父块元素的高度（不建议使用）

- 在父块中添加一个空的div，设置margin和padding都为0px，并清除左右浮动

  ```html
  <div class="clear"></div>
  
  <style>
    .clear{
      margin: 0px;
      padding: 0px;
      clear: both;
    }
  </style>
  ```

  页面效果：

  ![image-20200719201746589](https://images.shiguangping.com/imgs/20200719201746.png)

  给这个空的div添加个边框就可以看出效果，空div清除左右浮动之后，它就会跑到其他浮动元素的下方，这样就会把父级div撑开，并且高度会随着其他元素自动调整。

- 在父块元素中添加`overflow`属性

- 在父块元素添加伪类`:after`（推荐使用）

  ```css
  #father:after{
    /*添加空文本*/
    content: '';
    /*空文本以块元素方式显示*/
    display: block;
    /*清除左右浮动*/
    clear: both;
  }
  ```

  

#### `overflow`属性：

overflow属性指定如果内容溢出一个元素的框，会发生什么。

属性值

| 值      | 描述                                                     |
| ------- | -------------------------------------------------------- |
| visible | 默认值。内容不会被修剪，会呈现在元素框之外。             |
| hidden  | 内容会被修剪，并且其余内容是不可见的。                   |
| scroll  | 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。 |
| auto    | 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。 |
| inherit | 规定应该从父元素继承 overflow 属性的值。                 |