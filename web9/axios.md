# Vue.js Axios

axios是一个开源的可以用在浏览器和NodeJS的异步通信框架，它的主要作用是ajax异步通信，其功能特点如下：

- 在浏览器中创建`XMLHttpRequest`
- 从node.js创建http请求
- 支持Promise API [JS中链式编程]
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换JSON
- 客户端支持防御XSRF（跨站请求伪造）



```js
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            items: ["java", "Linux", "前端"],
        },
        data(){
          return{
              info:{
                  name:null,
                  age:null,
              }
          }
        },
        mounted() {
            axios.get("./json/data.json").then(res => (this.info=res.data), res => (alert("请求失败")))
        }
    })
</script>
```



### 在Vue项目中引入

1. 安装axios依赖

2. ```jsx
   import axios from 'axios'
   ```

3. ```js
   Vue.prototype.$http = axios
   ```

4. ```js
   mounted() {
     axios.get("./json/data.json").then(res => (this.info=res.data), res => (alert("请求失败")))
   }
   ```

   具体的使用方式和vue-resource非常类似



### axios常用请求方法：

```
get: 一般用于获取数据
post: 提交数据（表单提交、文件上传...）
put: 更新数据（所有数据都推送到服务端）
patch: 更新数据（只将修改的数据推送到服务端）
delete: 删除数据
```



### GET请求：

第一种写法：

```javascript
// 请求地址：http://localhost:8080/data.json?id=1
axios.get('/data.json',{params:{id:1}}).then(res => {
  console.log(res)
})
```

第二种写法：

```javascript
axios({
  method: 'get',
  url: '/data.json',
  params: {id:2}
}).then(res =>{
  console.log(res)
})
```



### POST请求：

提交参数的两种格式：

- form-data 表单提交（图片上传，文件上传）
- application/json

application/json格式：

```javascript
let data = {id: 12}
axios.post('/post', data).then(res => {
  console.log(res)
})
```

或者：

```javascript
let data = {id: 12}
axios({
  method: 'post',
  url: '/post',
  data: data
}).then(res => {
  console.log(res)
})
```

请求头：`Content-Type: application/json;charset=UTF-8`

---

form-data格式数据：

```javascript
let data = {id: 12}
// form-data请求
// 实例化form-data格式数据，将数据从data对象中遍历出来放到formData中
let formData = new FormData()
for(let key in data){
  formData.append(key, data[key])
}
axios.post('/post',formData).then(res =>{
  console.log(res)
})
```

请求头：`Content-Type: multipart/form-data;`



### PUT/PATCH请求：

提交参数的两种格式：

- form-data 表单提交（图片上传，文件上传）
- application/json

```javascript
// put请求
axios.put('/put',data).then(res =>{
  console.log(res)
})
// patch请求
axios.patch('/patch',data).then(res =>{
  console.log(res)
})
```

第二种写法同上。



### DELETE请求：

delete请求和get请求一样，`axios.delete(url,config)`两个参数

```javascript
// 参数拼接在url上
axios.delete('/delete',{params:{id:13}}).then(res =>{
  console.log(res)
})

// 参数不拼接在url上
axios.delete('/delete',{data:{id:123}}).then(res =>{
  console.log(res)
})
```



### 并发请求：

同时进行多个请求，并统一处理返回值

```javascript
//axios.all()并发请求， axios.spread()处理响应
axios.all([
  axios.get('/data.json'),
  axios.get('/city.json')
]).then(
  axios.spread((dataRes,cityRes)=>{
    console.log(dataRes,cityRes)
  })
)
```



### Axios创建实例：

如果需要访问不同的后端域名接口，可以创建多个axios实例，每个实例绑定不同的域名和其他配置：

```javascript
// axios可以创建多个实例，每个实例绑定不同的请求域名或配置
let instance1 = axios.create({
  baseURL: 'http://localhost:8080',
  timeout: 1000
})
let instance2 = axios.create({
  baseURL: 'http://localhost:9090',
  timeout: 5000
})

instance1.get('/data.json').then(response => {
  console.log(response)
})
instance2.get('/data.json').then(response => {
  console.log(response)
})
```



axios常用配置参数：

```javascript
axios.create({
  baseURL: 'http://localhost:8080',// 请求的基本地址
  timeout: 1000,// 设置请求超时时长ms
  url: '/data.json',// 请求的资源路径
  method: 'get,post,put,patch,delete',// 请求方法
  headers: {
    token: '123asd'
  },// 设置请求头
  params: {},// 会将请求参数拼接到url中
  data: {},// 请求参数在请求体中
})
```

都在哪里可以配置axios的参数：

```javascript
// 1. axios全局配置
axios.defaults.timeout = 1000
axios.defaults.baseURL = 'http://localhost'

// 2. axios实例配置
let instance = axios.create({
  baseURL: 'http://localhost:8080',
})
instance.defaults.timeout = 2000

// 3. axios请求配置
instance.get('/data.json', {timeout: 5000, params: {id: 1}})
```

优先级从低到高 `全局<实例<请求`



### 拦截器：

**请求拦截器：**（请求没到后端，如404）

```javascript
// 请求拦截器
axios.interceptors.request.use(config => {
  // 在发送请求前doSomething
  return config
}, error => {
  // 在请求错误时doSomething
  return Promise.reject(error)
})
```

**响应拦截器：**（请求到达后端）

```javascript
// 响应拦截器
axios.interceptors.response.use(res => {
  // 请求成功后，对响应数据做处理
  return res
}, error => {
  // 响应错误，对响应数据做处理
  return Promise.reject(error)
})
```

**拦截器中return的数据都到哪了？**

```javascript
axios.get('/data.json')
  .then(res => {
  // 响应拦截器，return的res就返回到这里
  console.log(res)
}).catch(err => {
  // 响应拦截器中，return Promise.reject(error)就返回到这里
  console.log(err)
})
```

**取消拦截器：**

```javascript
// 取消拦截器（了解）
let interceptor = axios.interceptors.request.use(config=>{
  config.headers = {auth:true}
  return config
})
// 取消定义的拦截器
axios.interceptors.request.eject(interceptor)
```

