# 5. Ajax

Asynchronous JavaScript + XML（异步JavaScript和XML）

- 同步：必须等待前面的任务完成，才能继续后面的任务
- 异步：不受当前任务的影响

### XMLHttpRequest

`XMLHttpRequest`（XHR）对象用于与服务器交互。通过 XMLHttpRequest 可以在不刷新页面的情况下请求特定 URL，获取数据。这允许网页在不影响用户操作的情况下，更新页面的局部内容。`XMLHttpRequest` 在 [AJAX](https://developer.mozilla.org/zh-CN/docs/Glossary/AJAX) 编程中被大量使用。

##### 构造函数：

`XMLHttpRequest()`

该构造函数用于初始化一个 `XMLHttpRequest` 实例对象。在调用下列任何其他方法之前，必须先调用该构造函数，或通过其他方式，得到一个实例对象。



### 使用Ajax发送请求

AJAX的核心js对象就是XMLHttpRequest，发送Ajax请求的五个步骤：

1. 创建异步对象XMLHttpRequest，`var req = new XMLHttpRequest();`
2. 设置请求的参数`req.open("POST", url, true);`包括请求方式，URL，是否是异步
3. 发送请求，`req.send(null);`，可以发送数据，也可以不发
4. 注册时间，`req.onreadystatechange`，当状态有改变时调用
5. 获取返回的数据



代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Ajax Demo</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
</head>
<body>
<table>
    <tr>
        <td>用户名：</td>
    </tr>
    <tr>
        <td><input type="text" id="name" onchange="onChangeShow()"></td>
    </tr>
</table>
</body>
<script type="text/javascript">

    let url = "TestServlet";
    var req;

    function onChangeShow() {
        if (window.XMLHttpRequest) {
            req = new XMLHttpRequest();
        } else {
            req = new ActiveXObject();
        }

        if (req) {
            req.open("POST", url, true);
            req.onreadystatechange = function () {
                if (req.readyState == 4) {
                    if (req.status == 200) {
                        parseMessageByText();
                    } else {
                        alert("请求失败")
                    }
                }
            };
            req.send(null);
        }
    }

    function parseMessageByText() {
        document.getElementById("name").value = req.responseText;
    }
</script>
</html>
```



