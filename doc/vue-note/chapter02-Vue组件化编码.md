## chapter02-Vue组件化编码

### 一、使用 vue-cli 创建模板项目

#### 1.1、说明
```
vue-cli 是 vue 官方提供的脚手架工具 
github:https://github.com/vuejs/vue-cli 
作用: 从 https://github.com/vuejs-templates 下载模板项目
```

#### 1.2、创建vue项目
```
npm install -g vue-cli 
vue init webpack_vue_demo 
cd vue_demo 
npm install 
npm run dev 
访问:http://localhost:8080/
```

#### 1.3、模板项目的结构
```
|-- build                            // 项目构建(webpack)相关代码
|   |-- build.js                     // 生产环境构建代码
|   |-- check-version.js             // 检查node、npm等版本
|   |-- utils.js                     // 构建工具相关
|   |-- vue-loader.conf.js           // webpack loader配置
|   |-- webpack.base.conf.js         // webpack基础配置
|   |-- webpack.dev.conf.js          // webpack开发环境配置,构建开发本地服务器
|   |-- webpack.prod.conf.js         // webpack生产环境配置
|-- config                           // 项目开发环境配置
|   |-- dev.env.js                   // 开发环境变量
|   |-- index.js                     // 项目一些配置变量
|   |-- prod.env.js                  // 生产环境变量
|   |-- test.env.js                  // 测试脚本的配置
|-- src                              // 源码目录
|   |-- components                   // vue所有组件
|   |-- router                       // vue的路由管理
|   |-- App.vue                      // 页面入口文件
|   |-- main.js                      // 程序入口文件，加载各种公共组件
|-- static                           // 静态文件，比如一些图片，json数据等
|-- test                             // 测试文件
|   |-- e2e                          // e2e 测试
|   |-- unit                         // 单元测试
|-- .babelrc                         // ES6语法编译配置
|-- .editorconfig                    // 定义代码格式
|-- .eslintignore                    // eslint检测代码忽略的文件（夹）
|-- .eslintrc.js                     // 定义eslint的plugins,extends,rules
|-- .gitignore                       // git上传需要忽略的文件格式
|-- .postcsssrc                      // postcss配置文件
|-- README.md                        // 项目说明，markdown文档
|-- index.html                       // 访问的页面
|-- package.json                     // 项目基本信息,包依赖信息等
```

### 二、项目的打包和发布

#### 2.1、打包
npm run build

#### 2.2、发布 1: 使用静态服务器工具包
```
npm install -g serve 
serve dist 
访问:http://localhost:5000
```

#### 2.3、发布 2: 使用动态web服务器(tomcat)
修改配置:webpack.prod.conf.js
```
output:{ 
  publicPath:'/xxx/' //打包文件夹的名称 
} 
```

重新打包: npm run build

修改 dist 文件夹为项目名称:xxx 

将 xxx 拷贝到运行的 tomcat 的 webapps 目录下 

访问:http://localhost:8080/xxx


### 三、eslint
#### 3.1、说明
- ESLint 是一个代码规范检查工具 
- 它定义了很多特定的规则, 一旦你的代码违背了某一规则,eslint会作出非常有用的提示 
- 官网:http://eslint.org/ 
- 基本已替代以前的 JSLint

#### 3.2、ESLint 提供以下支持
- ES 
- JSX 
- style 检查
- 自定义错误和提示

#### 3.3、ESLint 提供以下几种校验
- 语法错误校验
- 不重要或丢失的标点符号，如分号
- 没法运行到的代码块（使用过 WebStorm 的童鞋应该了解） 
- 未被使用的参数提醒 
- 确保样式的统一规则，如 sass 或者 less 
- 检查变量的命名

#### 3.4、规则的错误等级有三种
- 0：关闭规则。
- 1：打开规则，并且作为一个警告（信息打印黄色字体） 
- 2：打开规则，并且作为一个错误（信息打印红色字体）

#### 3.5、相关配置文件
1) .eslintrc.js: 全局规则配置文件
```
'rules':{ 'no-new':1 }
```

在 js/vue 文件中修改局部规则 

2) /*eslint-disableno-new*/ 
```
newVue({ el:'body', components:{App} })
```

3) .eslintignore: 指令检查忽略的文件 
```
*.js 
*.vue
```

### 四、组件定义与使用
#### 4.1、vue 文件的组成部分

1) 模板页面 
```
<template> 页面模板 </template> 
```
2) JS 模块对象 
```
<script> 
export default{ 
  data(){return{}}, 
  methods:{}, 
  computed:{}, 
  components:{} 
} 
</script> 
```
3) 样式 
```
<style>
  样式定义 
</style>
```

#### 4.2、基本使用
1) 引入组件 
2) 映射成标签 
3) 使用组件标签 


### 五、组件间通信
#### 5.1、组件间通信基本原则
不要在子组件中直接修改父组件的状态数据 

数据在哪, 更新数据的行为(函数)就应该定义在哪

#### 5.2、vue 组件间通信方式
- props 
- vue 的自定义事件 
- 消息订阅与发布(如:pubsub 库) 
- slot 
- vuex(后面单独讲)

### 六、组件间通信 1:props
#### 6.1. 使用组件标签时
```
<my-componentname='tom':age='3':set-name='setName'></my-component>
```

#### 6.2. 定义 MyComponent 时
1) 在组件内声明所有的 props 
2) 方式一: 只指定名称 
```
props:['name','age','setName'] 
```
3) 方式二: 指定名称和类型 
```
props:{ 
  name:String, 
  age:Number, 
  setNmae:Function 
}
```
4) 方式三: 指定名称/类型/必要性/默认值 
```
props:{ 
  name:{type:String,required:true,default:xxx}
}
```

#### 6.3、注意
- 此方式用于父组件向子组件传递数据 
- 所有标签属性都会成为组件对象的属性, 模板页面可以直接引用 
- 问题: 
  - 如果需要向非子后代传递数据必须多层逐层传递
  - 兄弟组件间也不能直接 props 通信, 必须借助父组件才可以


### 七、组件间通信 2:vue 自定义事件
#### 7.1、绑定监听事件
```
// 方式一: 通过 v-on 绑定 
@delete_todo="deleteTodo" 
// 方式二: 通过$on() 
this.$refs.xxx.$on('delete_todo',function(todo){ this.deleteTodo(todo) })
```

#### 7.2、触发事件
```
// 触发事件(只能在父组件中接收) 
this.$emit(eventName,data)
```

#### 7.3、注意
此方式只用于子组件向父组件发送消息(数据) 

问题: 隔代组件或兄弟组件间通信此种方式不合适


### 八、组件间通信 3: 消息订阅与发布(PubSubJS 库)
#### 8.1、订阅消息
```
PubSub.subscribe('msg',function(msg,data){})
```

#### 8.2、发布消息
```
PubSub.publish('msg',data)
```

#### 8.3、注意
优点: 此方式可实现任意关系组件间通信(数据)

#### 8.4、事件的 2 个重要操作(总结)
1) 绑定事件监听 (订阅消息) 
```
目标: 标签元素 <button> 
事件名(类型):click/focus 
回调函数:function(event){}
```
2) 触发事件 (发布消息)           
DOM 事件: 用户在浏览器上对应的界面上做对应的操作      
自定义: 编码手动触发   


### 九、组件间通信 4:slot
#### 9.1、理解
此方式用于父组件向子组件传递`标签数据`

#### 9.2、子组件:Child.vue
```
<template>
  <div>
    <slotname ="xxx">不确定的标签结构 1</slot>
    <div>组件确定的标签结构</div>
    <slotname ="yyy">不确定的标签结构 2</slot> </div>
</template>
```

#### 9.3、父组件:Parent.vue
```
<child>
  <div slot ="xxx">xxx 对应的标签结构</div>
  <div slot ="yyy">yyyy 对应的标签结构</div> 
</child>
```

