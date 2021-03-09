## chapter03-vue-ajax

### 一、vue 项目中常用的 2 个 ajax 库
vue-resource：   
vue 插件, 非官方库,vue1.x 使用广泛

axios：   
通用的 ajax 请求库, 官方推荐,vue2.x 使用广泛

### 二、vue-resource 的使用
#### 2.1、在线文档
https://github.com/pagekit/vue-resource/blob/develop/docs/http.md

#### 2.2、下载
npm install vue-resource --save

#### 2.3、编码
```
// 引入模块 
importVueResourcefrom'vue-resource' 
// 使用插件 
Vue.use(VueResource)

// 通过 vue/组件对象发送 ajax 请求 
this.$http.get('/someUrl').then((response)=>{ 
  //successcallback 
  console.log(response.data)
  //返回结果数据 },(response)=>{ 
  //errorcallback
  console.log(response.statusText)//错误信息
})
```

### 三、axios 的使用
#### 3.1、在线文档
https://github.com/pagekit/vue-resource/blob/develop/docs/http.md

#### 3.2、下载
npm install axios --save

#### 3.3、编码
```
// 引入模块 
importaxiosfrom'axios'
// 发送 ajax 请求 
axios.get(url) 
.then(response=>{ console.log(response.data)// 得到返回结果数据
 }) 
.catch(error=>{ console.log(error.message) })
```

#### 3.4、测试接口：   
```
接口 1:https://api.github.com/search/repositories?q=v&sort=stars     
接口 2:https://api.github.com/search/users?q=aa
```

