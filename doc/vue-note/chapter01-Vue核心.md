## chapter01-Vue核心

### 一、Vue 基本认识

#### 1.1、官网
- 英文官网:https://vuejs.org/
- 中文官网:https://cn.vuejs.org/

#### 1.2、介绍描述
- 渐进式 JavaScript 框架 
- 作用: 动态构建用户界面

#### 1.3、特点
- 遵循 MVVM 模式
- 编码简洁, 体积小, 运行效率高, 适合移动/PC 端开发 
- 它本身只关注 UI, 可以轻松引入 vue 插件或其它第三库开发项目

#### 1.4、与其它前端 JS 框架的关联
- 借鉴 angular 的模板和数据绑定技术
- 借鉴 react 的组件化和虚拟 DOM 技术

#### 1.5、Vue 扩展插件
- vue-cli:vue 脚手架 
- vue-resource(axios):ajax 请求 
- vue-router: 路由
- vuex: 状态管理 
- vue-lazyload: 图片懒加载 
- vue-scroller: 页面滑动相关 
- mint-ui: 基于 vue 的 UI 组件库(移动端) 
- element-ui: 基于 vue 的 UI 组件库(PC 端)


### 二、Vue 的基本使用
```
<div id="app"> 
<input type="text" v-model="username"> 
<p>Hello, {{username}}</p> 
</div>

<script type="text/javascript" src="../js/vue.js"></script>
<script type="text/javascript"> 
  new Vue({
  el: '#app', 
  data: {username: 'atguigu'}
}) 
</script>
```

### 三、模板语法
#### 3.1、模板的理解
- 动态的 html 页面 
- 包含了一些 JS 语法代码 
  - 双大括号表达式 
  - 指令(以 v-开头的自定义标签属性)

#### 3.2、双大括号表达式
- 语法: {{exp}} 
- 功能: 向页面输出数据 
- 可以调用对象的方法

#### 3.3、指令一: 强制数据绑定
- 功能: 指定变化的属性值 
- 完整写法: v-bind:xxx='yyy' //yyy 会作为表达式解析执行
- 简洁写法: :xxx='yyy'

#### 3.4、指令二: 绑定事件监听
功能: 绑定指定事件名的回调函数 

```
完整写法: 
v-on:keyup='xxx' 
v-on:keyup='xxx(参数)' 
v-on:keyup.enter='xxx' 

简洁写法: 
@keyup='xxx' 
@keyup.enter='xxx'
```

### 四、计算属性和监视

#### 4.1、计算属性
在 computed 属性对象中定义计算属性的方法 

在页面中使用{{方法名}}来显示计算的结果

#### 4.2、监视属性
通过通过 vm 对象的$watch()或 watch 配置来监视指定的属性 

当属性变化时, 回调函数自动调用, 在函数内部进行计算

#### 4.3、计算属性高级
通过 getter/setter 实现对属性数据的显示和监视 

计算属性存在缓存, 多次读取只执行一次 getter 计算


### 五、class 与 style 绑定

#### 5.1、理解
在应用界面中, 某个(些)元素的样式是变化的 

class/style 绑定就是专门用来实现动态样式效果的技术

#### 5.2、class 绑定
- :class='xxx' 
- 表达式是字符串:'classA' 
- 表达式是对象:{classA:isA,classB:isB} 
- 表达式是数组:['classA','classB']

#### 5.3、style 绑定
- :style="{color:activeColor,fontSize:fontSize+'px'}" 
- 其中 activeColor/fontSize 是 data 属性


### 六、条件渲染
#### 6.1、条件渲染指令
- v-if 与 v-else 
- v-show

#### 6.2、比较 v-if 与 v-show
如果需要频繁切换 v-show 较好 

当条件不成立时,v-if 的所有子节点不会解析(项目中使用)


### 七、列表渲染
列表显示指令 数组:v-for/index 对象:v-for/key


### 八、事件处理

#### 8.1、绑定监听
```
v-on:xxx="fun"
@xxx="fun" 
@xxx="fun(参数)"
默认事件形参:event 
隐含属性对象:$event
```

#### 8.2、事件修饰符
.prevent: 阻止事件的默认行为 event.preventDefault() 

.stop: 停止事件冒泡 event.stopPropagation()

#### 8.3、按键修饰符
.keycode: 操作的是某个 keycode 值的键 
.keyName: 操作的某个按键名的键(少部分)


### 九、表单输入绑定
#### 9.1、使用 v-model 对表单数据自动收集
- text/textarea 
- checkbox 
- radio 
- select

### 十、Vue 实例生命周期

#### 10.1、生命周期流程图
![vue_life.png](./images/vue_life.png)

#### 10.2、vue 生命周期分析
```
初始化显示 
*beforeCreate() 
*created() 
*beforeMount() 
*mounted() 

更新状态:this.xxx=value 
*beforeUpdate() 
*updated() 

销毁 vue 实例:vm.$destory() 
*beforeDestory() 
*destoryed()
```

#### 10.3、常用生命周期方法
created()/mounted(): 发送 ajax 请求, 启动定时器等异步任务 

beforeDestory(): 做收尾工作, 如: 清除定时器

### 十一、过渡&动画
#### 11.1、vue 动画的理解
操作 css 的 trasition 或 animation

vue 会给目标元素添加/移除特定的 class 

过渡的相关类名 
```
xxx-enter-active: 指定显示的 transition 
xxx-leave-active: 指定隐藏的 transition 
xxx-enter/xxx-leave-to: 指定隐藏时的样式
```

#### 11.2、基本过渡动画的编码
在目标元素外包裹<transitionname="xxx"> 

定义 class 样式：指定过渡样式:transition ，指定隐藏时的样式:opacity/其它


### 十二、过滤器

#### 12.1、理解过滤器
功能: 对要显示的数据进行特定格式化后再显示

注意: 并没有改变原本的数据, 可是产生新的对应的数据

#### 12.2、理解过滤器
定义过滤器
```
// 定义过滤器
Vue.filter('dateString', function (value, format='YYYY-MM-DD HH:mm:ss') {
  return moment(value).format(format);
})
```
使用过滤器
```
<div>{{myData|filterName}}</div> 
<div>{{myData|filterName(arg)}}</div>
```

### 十三、内置指令与自定义指令
#### 13.1、常用内置指令
- v:text: 更新元素的 textContent 
- v-html: 更新元素的 innerHTML 
- v-if: 如果为 true, 当前标签才会输出到页面
- v-else: 如果为 false, 当前标签才会输出到页面 
- v-show: 通过控制 display 样式来控制显示/隐藏 
- v-for: 遍历数组/对象 
- v-on: 绑定事件监听, 一般简写为@ 
- v-bind: 强制绑定解析表达式, 可以省略 v-bind
- v-model: 双向数据绑定 
- ref: 指定唯一标识,vue 对象通过$els 属性访问这个元素对象 
- v-cloak: 防止闪现, 与 css 配合:[v-cloak]{display:none}

#### 13.2、自定义指令
1. 注册全局指令
```
Vue.directive('my-directive', function(el, binding){
  el.innerHTML = binding.value.toupperCase()
})
```  
2. 注册局部指令
```
directives : {
  'my-directive' : {
      bind (el, binding) {
        el.innerHTML = binding.value.toupperCase()
      }
  }
}
```
3. 使用指令
v-my-directive='xxx'


### 十四、自定义插件
Vue 插件是一个包含 install 方法的对象

通过 install 方法给 Vue 或 Vue 实例添加方法, 定义全局指令等
```
(function (window) {
  const MyPlugin = {}
  MyPlugin.install = function (Vue, options) {
    // 1. 添加全局方法或属性
    Vue.myGlobalMethod = function () {
      console.log('Vue函数对象的myGlobalMethod()')
    }

    // 2. 添加全局资源
    Vue.directive('my-directive',function (el, binding) {
      el.textContent = 'my-directive----'+binding.value
    })

    // 4. 添加实例方法
    Vue.prototype.$myMethod = function () {
      console.log('vm $myMethod()')
    }
  }
  window.MyPlugin = MyPlugin
})(window)

```

