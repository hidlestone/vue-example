## 06-vue 里的 data 声明方式

在简单的vue实例中看到的Vue实例中data属性是如下方式展示的：
```
let app= newVue({
 
    el:"#app",
    data:{
        msg:''
    },
    methods:{
       
    }
})
```

在使用组件化的项目中使用的是如下形式：
```
export default{
    data(){
        return {
            showLogin:true,
            // def_act: '/A_VUE',
            msg: 'hello vue',
            user:'',
            homeContent: false,
        }
    },
    methods:{
       
    }
```

为何在大型项目中data需要使用return返回数据呢？

原因：不使用return包裹的数据会在项目的全局可见，会造成变量污染。使用return包裹后数据中变量只在当前组件中生效，不会影响其他组件。



