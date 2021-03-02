## 03-vue项目文件说明

### 一、package.json

#### 1.1、作用
package.json 文件其实就是对项目或者模块包的描述，里面包含许多元信息。比如项目名称，项目版本，项目执行入口文件，项目贡献者等等。npm install 命令会根据这个文件下载所有依赖模块。

#### 1.2、文件创建
- 手动创建：直接在项目根目录新建一个 package.json 文件，然后输入相关的内容。
- 自动创建：也是在项目根目录下执行 npm init，然后根据提示一步步输入相应的内容完成后即可自动创建。

#### 1.3、文件示例
```
{
  "name": "exchange",
  "version": "0.1.0",
  "author": "zhangsan <zhangsan@163.com>",
  "description": "第一个node.js程序",
  "keywords":["node.js","javascript"],
  "private": true,
  "bugs":{"url":"http://path/to/bug","email":"bug@example.com"},
  "contributors":[{"name":"李四","email":"lisi@example.com"}],
  "repository": {
		"type": "git",
		"url": "https://path/to/url"
	},
  "homepage": "http://necolas.github.io/normalize.css",
  "license":"MIT",
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-router-dom": "^5.0.1",
    "react-scripts": "3.0.1"
  },
  "devDependencies": {
    "browserify": "~13.0.0",
    "karma-browserify": "~5.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "bin": {
  "webpack": "./bin/webpack.js"
  },
  "main": "lib/webpack.js",
  "module": "es/index.js",
  "eslintConfig": {
    "extends": "react-app"
  },
  "engines" : { 
    "node" : ">=0.10.3 <0.12" 
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "style": [
  "./node_modules/tipso/src/tipso.css"
],
  "files": [
    "lib/",
    "bin/",
    "buildin/",
    "declarations/",
    "hot/",
    "web_modules/",
    "schemas/",
    "SECURITY.md"
  ]
}
```

#### 1.4、文件配置说明
```
name：项目/模块名称，长度必须小于等于214个字符，不能以"."(点)或者"_"(下划线)开头，不能包含大写字母。
version：项目版本。
author：项目开发者，它的值是你在https://npmjs.org网站的有效账户名，遵循“账户名<邮件>”的规则，例如：zhangsan zhangsan@163.com。
description：项目描述，是一个字符串。它可以帮助人们在使用npm search时找到这个包。
keywords：项目关键字，是一个字符串数组。它可以帮助人们在使用npm search时找到这个包。
private：是否私有，设置为 true 时，npm 拒绝发布。
license：软件授权条款，让用户知道他们的使用权利和限制。
bugs：bug 提交地址。
contributors：项目贡献者 。
repository：项目仓库地址。
homepage：项目包的官网 URL。
dependencies：生产环境下，项目运行所需依赖。
devDependencies：开发环境下，项目所需依赖。
scripts：执行 npm 脚本命令简写，比如 “start”: “react-scripts start”, 执行 npm start 就是运行 “react-scripts start”。
bin：内部命令对应的可执行文件的路径。
main：项目默认执行文件，比如 require(‘webpack’)；就会默认加载 lib 目录下的 webpack.js 文件，如果没有设置，则默认加载项目跟目录下的 index.js 文件。
module：是以 ES Module(也就是 ES6)模块化方式进行加载，因为早期没有 ES6 模块化方案时，都是遵循 CommonJS 规范，而 CommonJS 规范的包是以 main 的方式表示入口文件的，为了区分就新增了 module 方式，但是 ES6 模块化方案效率更高，所以会优先查看是否有 module 字段，没有才使用 main 字段。
eslintConfig：EsLint 检查文件配置，自动读取验证。
engines：项目运行的平台。
browserslist：供浏览器使用的版本列表。
style：供浏览器使用时，样式文件所在的位置；样式文件打包工具parcelify，通过它知道样式文件的打包位置。
files：被项目包含的文件名数组。
```


### 二、package-lock.json
npm 5.0版本之后，npm install后都会有一个package-lock.json 。

#### 2.1、作用
1、锁定安装时的包的版本号，需要上传到git，保证大家的依赖包一致。
 
2、package-lock.json 是在 `npm install`时候生成一份文件，用来记录当前状态下实际安装的各个npm package的具体来源和版本号。
 
3、它有什么用呢？因为npm是一个用于管理package之间依赖关系的管理器，它允许开发者在pacakge.json中间标出自己项目对npm各库包的依赖。你可以选择以如下方式来标明自己所需要库包的版本；例如：
```
"dependencies": {
 "@types/node": "^8.0.33",
},
```

这里面的 向上标号^是定义了向后（新）兼容依赖，指如果 types/node的版本是超过8.0.33，并在大版本号（8）上相同，就允许下载最新版本的 types/node库包，例如实际上可能运行npm install时候下载的具体版本是8.0.35。

大多数情况这种向新兼容依赖下载最新库包的时候都没有问题，可是因为npm是开源世界，各库包的版本语义可能并不相同，有的库包开发者并不遵守严格这一原则：相同大版本号的同一个库包，其接口符合兼容要求。这时候用户就很头疼了：在完全相同的一个nodejs的代码库，在不同时间或者不同npm下载源之下，下到的各依赖库包版本可能有所不同，因此其依赖库包行为特征也不同有时候甚至完全不兼容。

解决：     
因此npm最新的版本就开始提供自动生成package-lock.json功能，为的是让开发者知道只要你保存了源文件，到一个新的机器上、或者新的下载源，只要按照这个package-lock.json所标示的具体版本下载依赖库包，就能确保所有库包与你上次安装的完全一样。

#### 2.2、package.json 缺点

原来package.json文件只能锁定大版本，也就是版本号的第一位，并不能锁定后面的小版本，你每次npm install都是拉取的该大版本下的最新的版本，为了稳定性考虑我们几乎是不敢随意升级依赖包的，这将导致多出来很多工作量，测试/适配等，所以package-lock.json文件出来了，当你每次安装一个依赖的时候就锁定在你安装的这个版本。

那如果我们安装时的包有bug，后面需要更新怎么办？    
以前：在以前可能就是直接改package.json里面的版本，然后再npm install了。   
现在：但是5版本后就不支持这样做了，因为版本已经锁定在package-lock.json里了，所以我们只能npm install xxx@x.x.x  这样去更新我们的依赖，然后package-lock.json也能随之更新。






