# Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版

> 2018年补充，如果你 clone 或者 fork 本项目之后，不能运行，说明 package-lock.json 锁定的各个工具的版本和你本地的环境有冲突，没有关系，只需要删除这个文件，然后重新安装就可以了。

```
rm -rf node_modules package-lock.json
npm i
```
> 补充结束

2016年，我写了一系列的 VUE 入门教程，当时写这一系列博文的时候，我也只是一个菜鸟，甚至在写的过程中关闭了代码审查，否则通不过校验。

本来写这一系列的博文只是为了给自己看的，但没想到的是，这系列博文的点击量超过了2万以上，搜索引擎的排名也是非常理想，这让我诚惶诚恐，生怕我写的博文有所纰漏，误人子弟。

再者，这一年的发展，VUE 项目快速迭代，看着我一年前写的博文，很可能各种提示已经发生改变，对照着过时的资料，非常可能导致新手在学习的过程中产生不必要的困扰。

因此，本人决定，重写这个系列的博文，力求以简明、清晰、准确的图文以及代码描述，配合 github 的项目开源代码，给各位 VUE 新手提供一个高质量的入门文案。

以下为我写的博文：

1. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（一）基础知识概述](http://blog.csdn.net/fungleo/article/details/77575077)
2. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（二）安装 nodejs 环境以及 vue-cli 构建初始项目](http://blog.csdn.net/fungleo/article/details/77584701)
3. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（三）认识项目所有文件](http://blog.csdn.net/fungleo/article/details/77585205)
4. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（四）调整 App.vue 和 router 路由](http://blog.csdn.net/fungleo/article/details/77600798)
5. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（五）配置 Axios api 接口调用文件](http://blog.csdn.net/fungleo/article/details/77601270)
6. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（六）将接口用 webpack 代理到本地](http://blog.csdn.net/fungleo/article/details/77601761)
7. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（七）初识 *.vue 文件](http://blog.csdn.net/fungleo/article/details/77602914)
8. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（八）渲染一个列表出来先](http://blog.csdn.net/fungleo/article/details/77603537)
9. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（九）再把内容页面渲染出来](http://blog.csdn.net/fungleo/article/details/77604490)
10. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（十）打包项目并发布到子目录](http://blog.csdn.net/fungleo/article/details/77606216)
11. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（十一）阶段性小结](http://blog.csdn.net/fungleo/article/details/77606321)
12. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（十二）打包项目图片等资源的处理](http://blog.csdn.net/fungleo/article/details/77799057)
13. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（十三）集成 UEditor 百度富文本编辑器](http://blog.csdn.net/column/details/17076.html)
14. [Vue2+VueRouter2+Webpack+Axios 构建项目实战2017重制版（十四）在项目中使用 jQuery](http://blog.csdn.net/fungleo/article/details/77879328)

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```
