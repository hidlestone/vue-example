## 05-vue-router 基本使用

https://router.vuejs.org/zh/installation.html

### 一、路由
路由中有三个基本的概念 route, routes, router
- route  它是一条路由，由这个英文单词也可以看出来，它是单数， Home按钮  => home内容， 这是一条route,  about按钮 => about 内容， 这是另一条路由。
- routes 是一组路由，把上面的每一条路由组合起来，形成一个数组。[{home 按钮 =>home内容 }， { about按钮 => about 内容}]
- router 是一个机制，相当于一个管理者，它来管理路由。
- 客户端中的路由，实际上就是dom 元素的显示和隐藏。当页面中显示home 内容的时候，about 中的内容全部隐藏，反之也是一样。客户端路由有两种实现方式：基于hash 和基于html5 history api 。

### 二、vue-router中的路由也是基于上面的内容来实现的
在vue中实现路由还是相对简单的。因为我们页面中所有内容都是组件化的，我们只要把路径和组件对应起来就可以了，然后在页面中把组件渲染出来。

#### 2.1、页面实现（html模版中）
在vue-router中, 我们看到它定义了两个标签<router-link> 和<router-view>来对应点击和显示部分。<router-link> 就是定义页面中点击的部分，<router-view> 定义显示部分，就是点击后，区配的内容显示在什么地方。所以 <router-link> 还有一个非常重要的属性 to，定义点击之后，要到哪里去， 如：<router-link  to="/home">Home</router-link>

#### 2.2、js 中配置路由
首先要定义route,  一条路由的实现。它是一个对象，由两个部分组成： path和component.  path 指路径，component 指的是组件。如：{path:’/home’, component: home}
```
const routes = [
  { path: '/home', component: Home },
  { path: '/about', component: About }
]
```

最后创建router 对路由进行管理，它是由构造函数 new vueRouter() 创建，接受routes 参数。
```
const router = new VueRouter({
      routes // routes: routes 的简写
})
```

配置完成后，把router 实例注入到 vue 根实例中,就可以使用路由了
```
const app = new Vue({
  router
}).$mount('#app')
```

执行过程：当用户点击 router-link 标签时，会去寻找它的 to 属性， 它的 to 属性和 js 中配置的路径{ path: '/home', component: Home}  path 一一对应，从而找到了匹配的组件， 最后把组件渲染到 <router-view> 标签所在的地方。所有的这些实现才是基于hash 实现的。











