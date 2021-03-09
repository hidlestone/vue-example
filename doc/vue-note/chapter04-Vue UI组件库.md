## chapter04-Vue UI组件库

### 一、常用
1) MintUI: 
- 主页:http://mint-ui.github.io/#!/zh-cn 
- 说明: 饿了么开源的基于 vue 的移动端 UI 组件库 

2) Elment 
- 主页:http://element-cn.eleme.io/#/zh-CN 
- 说明: 饿了么开源的基于 vue 的 PC 端 UI 组件库

### 二、使用MintUI
下载:
```
npm install --save mint-ui
```

实现按需打包
```
1. 下载 npm install --save-dev babel-plugin-component 
2. 修改 babel 配置 
"plugins": ["transform-runtime",["component", [ 
  { "libraryName": "mint-ui", "style": true } 
]]]
```

mint-ui 组件分类
- 标签组件
- 非标签组件



