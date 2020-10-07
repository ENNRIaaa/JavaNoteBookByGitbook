# 1. HTML基础

1. 概念：

   - Hyper Text Markup Language 超文本标记语言

     - 超文本是用超链接的方法，将各种不同空间的文字信息组织在一起的网状文本。

     - 标记语言是由一个个标记（标签）组成的

       标记语言不是编程语言


### HTML标签：

1. html文档后缀为： .html	.htm
2. 标签分为：
   1. 围堵标签：有开始标签，有结束标签
   2. 自闭和标签：开始标签和结束标签在一起，如br hr
3. 标签可以嵌套
4. 在开始标签内可以定义属性，属性是由键值对构成，值要用引号引起来，单引和双引都可以
5. html不缺分大小写，但是建议使用小写

![image-20200530100843994](https://images.shiguangping.com/imgs/20200530100844.png)



### HTML 元素：

HTML元素值的是从开始标签（start tag）到结束标签（end tag）的所有代码。

*开始标签常被称为开放标签（opening tag），结束标签常称为闭合标签（closing tag）。*



**HTML 元素语法：**

- HTML 元素以*开始标签*起始
- HTML 元素以*结束标签*终止
- *元素的内容*是开始标签与结束标签之间的内容
- 某些 HTML 元素具有*空内容（empty content）*
- 空元素*在开始标签中进行关闭*（以开始标签的结束而结束）
- 大多数 HTML 元素可拥有*属性*



**嵌套的HTML元素**

大多数HTML元素可以嵌套（可以包含其他HTML元素）

HTML文档由嵌套的HTML元素组成

```html
<html>
  <body>
    <p>
      This is my first paragraph.
    </p>
  </body>
  
</html>
```



### HTML属性：

HTML标签可以拥有属性。属性提供了有关HTML元素的更多的信息。

属性总是以名称/值对的形式出现，例如：name = "value"。

属性总是在HTML元素的开始标签中规定。



示例：

```html
<a href="https://www.shiguangping.com">This is a link</a>
```

HTML链接由a标签定义，链接的地址在href属性中



### HTML文档结构：

```html
<!DOCTYPE html>
<html lang="en">
<!--html文档语-->

<head>
    <!--head头标签
        title标签：标题标签-->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <!--body体标签：包含也页面所有的可见元素-->

</body>

</html>
```

HTML4.01文档声明方式：

<img src="https://images.shiguangping.com/imgs/20200530101704.png" alt="image-20200530101704841" width="450px"/>

HTML5文档声明方式：

<img src="https://images.shiguangping.com/imgs/20200530101729.png" alt="image-20200530101729907" width="450px" />

*注意：在HTML5中写HTML4.01的代码是兼容的（向后兼容），在HTML4.01中写HTML5的代码，会出问题。*



### HTML中的常用标签：

- 标题标签：h1-h6

- 段落标签：p

- 强调：strong，表示强调，有加粗效果，比较常用；em：也表示强调，内容会变成斜体

- 换行：br（自闭合标签）

  *补充：空白折叠：HTML文档中如果出现多个连续的空格或者有换行，浏览器会把这些空格或换行折叠成一个空格显示。*

- 水平分割线：hr（自闭合标签）

- 无序列表：ul（unordered list），里面嵌套li标签，代表每一条

- 有序标签：ol（ordered list），里面嵌套li标签

- 定义列表：dl（definition list），其中的子标签dt（definition title）定义标题，dd（definition description）定义列表描述

- 表格标签：table标签：

  - 子标签：行：tr，列：td，标题：th
  - 在table标签内，tr标签外使用caption标签为表格添加标题
  - 横向合并（合并列）：在th或者td标签中使用colspan属性，colspan="2"，合并两列
  - 纵向合并（合并行）：在td标签中使用rowspan属性，rowspan="2"，合并两行

- 链接标签：a（anchor）锚点，常用属性:

  - href：锚点链接
  - title：标题，鼠标放到超链接上显示的标题
  - target：超链接打开方式，target="_blank" 在新标签中打开链接
  - 通过a标签指向邮箱地址href="mailto:xxx@qq.com"

- 图像标签：img（自闭合标签）：

  - src属性：指向图片路径
  - width属性：图片宽度
  - height属性：图片高度
  - alt属性：当图片资源加载失败时，显示该属性指定的文本
  - title属性：鼠标悬浮式，显示title文本

- 表单标签：form:

  - action属性：表单提交的目的地
  - method属性：提交方式，常用为get、post，默认的提交方式是get

- 文本输入框：input标签（自闭合标签）：

  - type属性：文本输入框类型，如text、password、submit

    text：文本输入框

    password：密码输入框

    submit：表单提交按钮

    reset：表单重置按钮

    radio：单选框，如果需要多个单选框组合实现单选，那么这几个单选框要设置相同的name属性

    checkbox：复选框，如果需要多个复选框组合使用，那么这几个复选框要设置相同的name属性

  - value属性：文本框的值，文本输入框type为按钮时，value值为按钮显示的文本

  - placeholder属性：文本框中用于提示的文本

  - checked属性：单选框、复选框默认为选中状态，checked="checked"

- lable标签，通过lable中的for属性关联文本输入框中的id属性，可以实现关联。点击 label 元素内的文本，则会将鼠标切换到关联控件本身

- 下拉菜单：select标签，里面要使用option标签设置每个选择项

- 文本域输入框：textarea标签

  - rows属性：文本域默认显示的行数（高度）
  - cols属性：文本域默认显示的列数（宽度）

- div标签：（division），块标签（一个标签占用一行）本身没有任何样式，常与css搭配使用

- span标签：内联标签，本身没有任何样式，常与css搭配使用

