#项目代码结构
README.md           项目说明文件
package.json        第三方模块依赖
package-lock.json   第三方包的版本
*index.html          首页①*
.postcssrc.js       postcss配置项
.gitignore          git上传忽略文件
.eslintrc.js        代码规范检测
.eslintignore       不被检测代码规范的文件
.editorconfig       编辑器代码格式
.babelrc            语法转换,使浏览器能够懂
static              静态资源,图片,json数据等
node_modules        依赖的包  
src                 项目源代码
    *main.js         项目入口文件②*
    *App.vue         根组件,单文件组件,名字为App的组件③*
    *router/index.js 路由文件④*
    components      组件
        *HelloWorld.vue⑤*
    assets          项目资源
config              项目配置信息
    index.js        基础配置信息,写明路由指向的组件文件
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
*同一个页面编写时,创建子组件vue,然后引入注册和使用*
*main.js引vue,引css,引字体css等*
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
#首页Header区域开发
sudo npm install stylus --save
sudo npm install stylus-loader --save
pages
    home
        components
            Header.vue
    Home.vue   
*Home.vue里添加*            
import HomeHeader from './components/Header'
components:{
    HomeHeader
}
<home-header></home-header>
*Header.vue添加*
<style lang="stylus" scoped>
使用stylus,使用scoped确保不影响其他
reset中html的font-size为50px,则1rem相对与50px
如果尺寸图为2倍图,则量的100px,转化为正常50px,即1rem
设置line-height垂直居中
设置hight保证高度
flex弹性布局
http://www.runoob.com/w3cnote/flex-grammar.html
#iconfont的使用和代码优化
*使用iconfont图标*,加入购物车,添加到项目,下载至本地
iconfont.js及demo文件不用
修改iconfont.css的目录,删除拼音,使用时到网站复制代码
在main.js引入
<span class="iconfont">&#xe624;</span>
*创建varibles.styl文件优化*,把基础背景颜色等变量写入
在vue中引用    @import '~@/assets/styles/varibles.styl' 在vue的style里加@及~
*在webpack.base.conf.js里可以给路径起别名优化*
 'styles' :resolve('src/assets/styles'),
 @import '~styles/varibles.styl'
重启npm run start
