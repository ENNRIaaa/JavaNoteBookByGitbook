# yaml配置文件

SpringBoot的核心配置文件：

`application.properties`：

- 语法格式：key=value

`application.yaml`或者`application.yml`：

- 语法格式：key: value    (:冒号后面有一个空格+value)



# YAML

维基百科，自由的百科全书

**YAML**（[/ˈjæməl/](https://zh.wikipedia.org/wiki/Help:英語國際音標)，尾音类似*camel*骆驼）是一个可读性高，用来表达数据[序列化](https://zh.wikipedia.org/wiki/序列化)的格式。YAML参考了其他多种语言，包括：[C语言](https://zh.wikipedia.org/wiki/C語言)、[Python](https://zh.wikipedia.org/wiki/Python)、[Perl](https://zh.wikipedia.org/wiki/Perl)，并从[XML](https://zh.wikipedia.org/wiki/XML)、电子邮件的数据格式（RFC [2822](http://www.rfc-editor.org/rfc/rfc2822.txt)）中获得灵感。Clark Evans在2001年首次发表了这种语言[[1\]](https://zh.wikipedia.org/wiki/YAML#cite_note-1)，另外Ingy döt Net与Oren Ben-Kiki也是这语言的共同设计者[[2\]](https://zh.wikipedia.org/wiki/YAML#cite_note-2)。目前已经有数种编程语言或脚本语言支持（或者说解析）这种语言。

*YAML*是"YAML Ain't a Markup Language"（YAML不是一种[标记语言](https://zh.wikipedia.org/wiki/标记语言)）的[递归缩写](https://zh.wikipedia.org/wiki/遞迴縮寫)。在开发的这种语言时，*YAML* 的意思其实是："Yet Another Markup Language"（仍是一种[标记语言](https://zh.wikipedia.org/wiki/标记语言)）[[3\]](https://zh.wikipedia.org/wiki/YAML#cite_note-YAML_spec_2001_08_01-3)，但为了强调这种语言以数据做为中心，而不是以标记语言为重点，而用反向缩略语重命名。



```yaml
# 普通的键值对
name: liyan

# 对象
student:
  name: liyan
  age: 27

# 行内写法
student1: {name: liyan,age: 27}

# 数组
fruits:
  - apple
  - banana

pets: [cat,dog]
```

