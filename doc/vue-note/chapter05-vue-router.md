## chapter05-vue-router

### 一、理解
#### 1.1、说明
- 官方提供的用来实现 SPA 的 vue 插件 
- github:https://github.com/vuejs/vue-router 
- 中文文档:http://router.vuejs.org/zh-cn/ 
- 下载:npminstallvue-router--save

#### 1.2、相关API说明
1) VueRouter(): 用于创建路由器的构建函数 
```
newVueRouter({ 
  // 多个配置项 
}) 
```
2) 路由配置 
```
routes:[ 
  {
    // 一般路由 
    path:'/about', 
    component:About 
  }, 
  {// 自动跳转路由 
    path:'/', 
    redirect:'/about'   
} ] 
```
3) 注册路由器
```
import router from'./router' 
new Vue({ router }) 
```
4) 使用路由组件标签 
```
<router-link>: 用来生成路由链接 <router-linkto="/xxx">GotoXXX</router-link> 

<router-view>: 用来显示当前路由组件界面 <router-view></router-view>
```

### 二、基本路由
#### 2.1、路由组件
Home.vue    
About.vue

#### 2.2、应用组件：App.vue
```

<div>
  <!--路由链接--> 
  <router-linkto="/about">About</router-link> 
  <router-linkto="/home">Home</router-link> 
  <!--用于渲染当前路由组件--> 
  <router-view></router-view>
</div>
```

#### 2.3、路由器模块:src/router/index.js
```
export default new VueRouter({
  // 注册应用中所有的路由
  routes: [
    {
      path: '/about',
      component: About
    },
    {
      path: '/home',
      component: Home
    },
    {
      path: '/',
      redirect: '/about'
    }
  ]
})
```

#### 2.4、注册路由器：main.js
```
import Vue from 'vue'
import router from './router'
import App from './App.vue'

/* eslint-disable no-new */
new Vue({
  el: '#app',
  components: {App}, // 映射组件标签
  template: '<App/>', // 指定需要渲染到页面的模板
  router // 注册路由器
})
```

#### 2.5、总结：编写使用路由的3步
- 定义路由组件
- 注册路由 
- 使用路由 
  - <router-link> 
  - <router-view>


### 三、嵌套路由
#### 3.1、子路由组件
News.vue    
Message.vue   

#### 3.2、配置潜逃路由：router.js
```
{
  path: '/home',
  component: Home,
  children: [
    {
      path: '/home/news',
      component: News
    },
    {
      path: 'message',
      component: Message
    },
    {
      path: '',
      redirect: '/home/news'
    }
  ]
}
```

#### 3.3、路由连接：Home.vue
```
<router-linkto="/home/news">News</router-link> 
<router-linkto="/home/message">Message</router-link> 
<router-view></route-view>
```

### 四、向路由组件传递数据
#### 4.1、方式 1: 路由路径携带参数(param/query)
1) 配置路由
```
children: [
  {
    path:'detail/:id',
    component: MessageDetail
  }
]
```

2) 路由路径
```
<router-link :to="`/home/message/detail/${m.id}`">{{m.title}}</router-link>
或者
<router-link:to="'/home/message/mdetail/'+m.id">{{m.title}}</router-link> 
```

3) 路由组件中读取请求参数 
```
this.$route.params.id
```

#### 4.2、方式 2:<router-view>属性携带数据
```
<router-view:msg="msg"></router-view>
```

### 五、缓存路由组件对象
#### 5.1、理解
默认情况下, 被切换的路由组件对象会死亡释放, 再次回来时是重新创建的 

如果可以缓存路由组件对象, 可以提高用户体验

#### 5.2、编码实现
```
<keep-alive>
  <router-view msg="abc"></router-view>
</keep-alive>
```

### 六、编程式路由导航
#### 6.1、相关API
- this.$router.push(path): 相当于点击路由链接(可以返回到当前路由界面) 
- this.$router.replace(path): 用新路由替换当前路由(不可以返回到当前路由界面) 
- this.$router.back(): 请求(返回)上一个记录路由 
- this.$router.go(-1): 请求(返回)上一个记录路由 
- this.$router.go(1): 请求下一个记录路由

