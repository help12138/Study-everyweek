# axios
    axios 是基于promise对ajax的一种封装

    ajax ---> mvc

    axios ---> mvvm
## axios的基本使用
```JS
// 使用默认方式发送无参请求
  // 使用框架的话无需这样引入,但是需要安装对应库
  <script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios({
      url:"文档地址",
      methods: 'get'  // 不写默认是get请求,也可以把get换为post请求
    }).then(res => {
      console.log(res)
    })
  </script>
```
```JS
// 使用默认方式发送有参请求
  // 使用框架的话无需这样引入,但是需要安装对应库
  <script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    // 默认get请求方式
    axios({
      url: "接口地址",
      methods: 'post', // 改为post请求方式
      params:{
        id: '1',
        name: '张三'
      }
      // data:{
      //   name: '张三'
      // }
    }).then(res => {
      console.log(res)
    })
  </script>
```
后台控制器接收到的name null axios 使用post 携带参数请求默认使用application/json
* 解决方式一: params属性进行数据的传递
* 解决方式二: name=张三
* 解决方式三:服务器端给接收的参数加上@requestBody
## axios 请求方式
```JS
// 使用axios.get或者axios.post方式发送 无参请求
  <script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios.get('接口地址',).then(res => {
      console.log(res)
    }).catch(err => {
      console.log(err)
    })
  </script>
```
```JS
// 使用axios.get或者axios.post方式发送 有参请求
  <script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
  // 此处如果用post方式,那参数传递就要换为 'name=张三&age=10'
    axios.get('接口地址',{params:{id: 1}}).then(res => {
      console.log(res)
    }).catch(err => {
      console.log(err)
    })
  </script>
```
## axios的并发请求
```JS
// axios的并发请求
  <script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios.all([
      axios.get('接口地址'),
      axios.get('接口地址',{params:{id: 1}})
    ]).then(res => { // 请求成功响应的是一个数组
      console.log(res)
    }).catch(err => {
      console.log(err)
    })
  </script>
```
```JS
// 使用spread的方法处理
  <script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios.all([
      axios.get('接口地址'),
      axios.get('接口地址',{params:{id: 1}})
    ]).then(
      axios.spread((res1, res2)=>{
        console.log(res1)
        console.log(res2)
      })
    ).catch(err => {
      console.log(err)
    })
  </script>
```
## axios的全局配置
```JS
<script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios.defaults.baseURL = '接口地址公共位置' // 配置全局属性
    axios.defaults.timeout = 5

    axios.get('接口地址后面不同的').then(res => { // 在全局配置的基础上去网络请求
      console.log(res)
    })

    axios.post('接口地址后面不同的').then(res => {
      console.log(res)
    }).catch(err => {
      console.log(err)
    })
  </script>
```
## axios的实例
```JS
<script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    let newvar1 = axios.create({
      baseURL: '公共接口地址1',
      timeout: 5000
    }); // 创建axios实例

    let newvar2 = axios.create([
      baseURL: '公共接口地址2',
      timeout: 5000
    ])

    newvar1({
      url: '后接地址1'
    }).then(res => {
      console.log(res)
    })

    newvar2({
      url: '后接地址2'
    }).then(res => {
      console.log(res)
    }).catch(err => {
      console.log(err)
    })
  </script>
```
## axios 拦截器
    axios给我们提供了两大类拦截器,
      一种是请求方向的拦截(成功请求,失败的),
      另一种是响应方向的(成功的, 失败的)
    拦截器的作用
      用于我们在网络请求的时候发起请求或者响应时对操作进行响应的处理
      发起请求是可以添加网页加载的动画 强制登录
      响应的时候可以进行响应的数据处理
```JS
<script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios.interceptors.request.use(config => {
      console.log("进入请求拦截器")
      console.log(config)
      return config
    }, err => {
      console.log('请求方向失败')
      console.log(err)
    })

    axios.get('接口地址').then(res => {
      console.log(res)
    })
  </script>
```
```JS
<script src="http://unpkg.com/axios/dist/axios.min.js"></script>
  <script>
    axios.interceptors.response.use(config => {
      console.log("进入拦截器")

      return config.data;
    }, err=>{
      console.log('响应方向失败');
      console.log(err);
    })

    axios.get('接口地址').then(res=>{
      console.log(res)
    })
  </script>
```
## axios封装
```JS
// 封装位置
export function request(config){
  let newVar = axios.create({
    baseURL: "公共接口地址",
    timeout: 5000
  })
}

// 调用位置
import {request} from '封装文件位置'
request({
  url: '页面地址'
}).then(res => {
  console.log(res)
})
```