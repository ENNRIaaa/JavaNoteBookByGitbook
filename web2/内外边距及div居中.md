# 2.8 内外边距及div居中

#### 外边距 `margin`：

```css
margin: style                  /*单值语法  所有边缘 */  举例： margin: 1em; 
margin: vertical horizontal    /*二值语法  纵向 横向 */  举例： margin: 5% auto; 
margin: top horizontal bottom  /*三值语法 上 横向 下*/  举例： margin: 1em auto 2em; 
margin: top right bottom left  /*四值语法 上 右 下 左*/  举例： margin: 2px 1em 0 auto; 
```

- **只有一个** 值时，这个值会被指定给全部的 **四个边**.
- **两个** 值时，第一个值被匹配给 **上和下**, 第二个值被匹配给 **左和右**.
- **三个** 值时，第一个值被匹配给 **上**, 第二个值被匹配给 **左和右**, 第三个值被匹配给 **下**.
- **四个** 值时，会依次按 **上、右、下、左** 的顺序匹配 (即顺时针顺序).

使div块居中:

```css
div{
  margin:0px auto;
}
```



#### 内边距`padding`：

内边距是元素内容到边框的距离，可以设置上下左右的内边距



CSS可以通过浏览器的开发者工具来调试，实时预览。



#### 盒子的计算方式：

计算盒子具体多大，margin+border+padding+内容



#### 上一节会员登录框样式：

```css
/*body总有一个8px的外边距*/
body {
  margin: 0px;
}

/*选择id=box的div，设置div宽度、边框border样式、背景颜色*/
#box {
  width: 300px;
  height: 150px;
  border: 1px rgb(0, 0, 0);
  border-radius: 10px;
  background-color: #8EC5FC;
  background-image: linear-gradient(62deg, #8EC5FC 0%, #E0C3FC 100%);
  /*外边距上下为0px，左右为auto，实现居中*/
  margin: 0px auto;
}

/*设置h2标题颜色*/
h2 {
  color: #2d3436;
  /*设置标题居中*/
  text-align: center;
  margin-bottom: 1px;
  /*标题的内上边距设置10px*/
  padding-top: 10px;
}

/*设置输入框的无边框，有圆角*/
form div input {
  border: none;
  border-radius: 5px;
}

/*设置form表单中div间的行高*/
form > div {
  line-height: 2;
  /*div中文本和输入框居中*/
  text-align: center;
}
```

样式：

<img src="https://images.shiguangping.com/imgs/20200719121716.png" alt="image-20200719121716906" width="350px" />