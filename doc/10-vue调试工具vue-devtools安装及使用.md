## 10-vue调试工具vue-devtools安装及使用

```
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! vue-devtools@5.3.3 build: `cd packages/shell-chrome &&  webpack --progress --hide-modules`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the vue-devtools@5.3.3 build script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
npm WARN Local package.json exists, but node_modules missing, did you mean to install?```
此原因是因为我们git clone时默认分支为最新的develop分支。develop是测试分支，不是正式分支，git时更换分支即可。
本人亲测v5.1.1分支是可用的，估计再向前的分支也是可用，当然master分支更是可用。(试过也不可用)
正确获取方法（使用分支:v5.1.1）
```

1、下载 v5.1.1
```
git clone -b v5.1.1 https://github.com/vuejs/vue-devtools.git
```

2、修改mainifest.json 中的persistant为true

3、安装依赖
```
npm i 或 cnpm install
```

4、构建
```
npm run build
```

5、chrome中找到 更多工具 / 扩展程序 选项，勾选 开发者模式，然后点击 加载已解压的扩展程序，选择vue-devtools\shells\chrome，确认

