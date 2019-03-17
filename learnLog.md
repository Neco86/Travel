#项目代码结构
README.md           项目说明文件
package.json        第三方模块依赖
package-lock.json   第三方包的版本
index.html          首页
.postcssrc.js       postcss配置项
.gitignore          git上传忽略文件
.eslintrc.js        代码规范检测
.eslintignore       不被检测代码规范的文件
.editorconfig       编辑器代码格式
.babelrc            语法转换,使浏览器能够懂
static              静态资源,图片,json数据等
node_modules        依赖的包  
src                 项目源代码
    *main.js         项目入口文件*
    *App.vue         根组件,单文件组件,名字为App的组件*
    router/index.js 路由文件
    components      组件
        HelloWorld.vue
    assets          项目资源
config              项目配置信息
    *index.js        基础配置信息,写明路由指向的组件文件*
    dev.env.js      开发环境配置信息
    prod.env.js     线上开发环境配置信息
build               打包配置内容
    webpack.base.conf.js
    webpack.dev.conf.js
    webpack.prod.conf.js
    ...
#单文件组件与Vue中的路由
import Vue from 'vue'
import App from './App'     App在的位置src/App.vue(自动补充后缀)
import router from './router'
src/main.js
new Vue({
  el: '#app',               挂载点app,在src/index.html里有 <div id="app"></div>
  router,                   ES6写法,路由:根据网址不同,返回不同的内容给用户,App.vue里<router-view/>显示的是当前路由地址所对应的内容
  components: { App },      ES6写法,与components: { App:App }一样,局部组件注册
  template: '<App/>'        模板显示App组件
})
*index.html(#app)----->main.js(el:'#app' template: '<App/>'入口文件)----->App.vue(根组件)中的路由标签(<router-view/>)----->index.js(配置信息,@指src目录)------>xxx.vue(子组件)*
#多页应用vs单页应用
多页应用                                                    单页应用(使用vue的为单页应用)
页面跳转->返回新的HTML                                        页面跳转->JS渲染
优点:首屏时间快,seo(搜索引擎优化)效果好                         优点:页面切换快
缺点:页面切换慢                                              缺点:首屏时间稍慢,SEO差

<template></template>只能暴露一个根标签
用<router-link to='/list'>列表页</router-link>来代替a标签
#项目代码初始化
在index.html中
    添加以下内容,实现移动端,用户不可缩放
    minimum-scale=1.0,maximum-scale=1.0,user-scalable=no
在main.js里修改引入
    引入reset.css
    引入border.css 移动端存在1px边框问题
    解决300ms移动延迟问题
        sudo npm install fastclick --save(--save指打包也用)
        引入fastclick:
            import fastClick from 'fastclick'
            fastClick.attach(document.body)
在https://www.iconfont.cn/ 图标管理/我的项目里创建项目
