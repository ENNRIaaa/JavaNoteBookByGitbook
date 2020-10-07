# slot插槽：内容分发

代码示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="js/vue.js"></script>
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.19.2/axios.js"></script>
</head>
<body>
<div id="app">
    <todo>
        <todo-title slot="todo-title" :title="title"></todo-title>
        <todo-items slot="todo-items" v-for="item in todoItems" :item="item"></todo-items>
    </todo>
</div>
</body>
<script>
    Vue.component('todo', {
        //slot用来定义插槽
        template: '<div>' +//slot通过name属性绑定要插入的组件
            '<slot name="todo-title"></slot>' +
            '<ul>' +
            '<slot name="todo-items"></slot>' +
            '</ul>' +
            '</div>'
    })

    Vue.component('todo-title', {
        props: ['title'],
        template: '<div>{{title}}</div>'
    })

    Vue.component('todo-items', {
        props: ['item'],
        template: '<li>{{item}}</li>'
    })

    var vm = new Vue({
        el: '#app',
        data: {
            title:'Java技术',
            todoItems:['JavaSE','Spring','SpringMVC','Mybatis']
        },
    })
</script>
</html>
```

