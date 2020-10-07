# vue组件

定义组件component：

JavaScript：

```js
<script>
		//定义组件
    Vue.component('liyan',{
        props:['item'],
        template:'<li>{{item}}</li>'
    })

    var vm = new Vue({
        el:'#app',
        data:{
            items:["java","Linux","前端"]
        }
    })
</script>
```



HTML：

```html
<div id="app">
    <liyan v-for="item in items" v-bind:item="item"></liyan>
</div>
```



- Vue全局对象.component()创建组件

- component()需要传递两个参数，一个是组件名，一个是属性对象

- 属性对象中有两个属性：
  - props：用于绑定数据
  - template：模板
- 在div中，使用自定义的组件标签循环tiems数组，通过v-bind绑定组件中的props属性，把循环的每一个值传进来

