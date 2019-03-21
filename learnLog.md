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
static              静态资源,图片,json数据等--------------------------------*存放模拟json数据*
node_modules        依赖的包  
src                 项目源代码
    *main.js         项目入口文件②*----------------------------------------*main.js引轮播图,引css,引字体css等*
    *App.vue         根组件,单文件组件,名字为App的组件③*----------------------*keepalive优化,减少ajax请求*
    *router/index.js 路由文件④*-------------------------------------------*多页面使用*
    components      组件
        *HelloWorld.vue⑤*-------------------------------------------------*即pages/x/x.vue 每个页面组件 及页面子组件*
    assets          项目资源------------------------------------------------*存放iconfont,x.styl*
config              项目配置信息
    index.js        基础配置信息,写明路由指向的组件文件-------------------------*修改模拟json数据位置*
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
*main.js引轮播图,引css,引字体css等*
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
<style lang="stylus" scoped></style>
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

git的使用 
        上传
        git add .添加到本地仓库
        git commit -m ''添加描述
        git push   推到github
        转换分支
        git pull
        git checkout index-swiper切换分支
        合并
        git checkout master
        git merge index-swiper
#首页轮播图
git创建分支branch
    点击branch创建index-swiper分支
    git pull
    git checkout index-swiper切换分支
    git status查看情况
git里查找vue-awesome-swiper(使用旧版的)
<style lang="stylus" scoped>
    .wrapper
        width: 100%
        height: 0
        overflow: hidden
        padding-bottom: 31.25%//宽高比
        .swiper-img
            width: 100%
</style>
轮播图中点改颜色
.wrapper >>> .swiper-pagination-bullet-active
因为写了scoped无法修改,所以用>>>来穿透
推到github上
git checkout master切换到master分支
git merge  origin/index-swiper合并


添加border-bottom的class即添加一像素边框
子元素不显示...,父元素添加min-width: 0

#Ajax获取首页数据
使用axios
sudo npm install axios --save
在Home.vue里添加
import axios from 'axios'
mounted () {
    this.getHomeInfo()
  }
}
methods: {
    getHomeInfo: function () {
        axios.get('/api/index.json').then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc: function (res) {
      console.log(res)
    }
添加文件
static/mock/index,json
网页只可以访问到static目录下文件
此为模拟数据,不希望上传
.gitignore里添加
static/mock

修改config/index.js
实现/api/index.json => /static/mock/index.js
proxyTable: {
        '/api': {
            target: 'http://localhost:8080',
            pathRewrite: {
                '^/api': '/static/mock'
            }
        }
    }
#首页父子组件数据传递
绑定数据
在Home.Vue添加
data () {
    return {
        city: ''
    }
  }
<home-header :city='city'></home-header>
在Header.vue添加
props: {
    city: String
  }
Home.vue修改
getHomeInfoSucc: function (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.city = data.city
      }
      console.log(res)
    }
  }
轮播图中点为最后一个,因为最开始获取的数据为空
添加
v-if='showSwiper'
computed: {
    showSwiper () {
      this.list.length
    }
  }
解决
#城市选择页面路由配置
router/index.js添加
{
      path: '/city',
      name: 'City',
      component: City
    }
import City from '@/pages/city/City'
<router-link to='/city'></router-link>
router-link会把颜色改为绿色

改一像素边框
.border-topbottom
     &:before
         border-color: #ccc
     &:after
         border-color: #ccc
#city-list
超出部分不要实现滚动,overflow:hidden
使用Better-scroll插件
github查找Better-sroll
npm install Better-scroll --save

ref标签属性,可以获取dom
<div class="list" ref="wrapper">
import Bscroll from 'better-scroll'
export default {
  name: 'CityList',
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  }
}
better-wrapper的github上说明wrapper下只有一个子元素可以滑动

v-for='(item,key) of cities循环对象时,第二个为key

alphabet.vue
methods: {
    handleLeterClick: function (e) {
      console.log(e.target.innerText)
    }
把alphabet里的值传给List
在list.vue里
 <div class="area" v-for='(item,key) of cities' :key='key' :ref='key'>
 watch: {
    letter () {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        this.scroll.scrollToElement(element)
      }
    }
  }

在Alphabet里添加滚动变化
@touchstart='handleTouchStart'
@touchmove='handleTouchMove'
@touchend='handleTouchEnd'

#使用Vuex实现数据共享
City.vue与Home.vue数据通信
Bus比较麻烦
使用Vuex
https://vuex.vuejs.org/vuex.png
State存放公用数据

改变数据:State => Vue Components =(Dispatch)=> Actions =(Commit)=> Mutations

npm install vuex --save
import Vue from 'vue'
import Vuex from 'vuex'
Vue.use(Vuex)
由于写的Vuex文件较多,不放在main.js下,创建src/store/index.js,然后在main.js里import,记得vue创建实例时,添加store
export default new Vuex.Store({
    states: {
        city: '北京'
    }
})
this.city修改为this.$store.states.city
#在相应vue派发
methods: {
    handleCityClick (city) {
        this.$store.dispatch('changeCity',city)
    }
  }
#在index.js下写actions
export default new Vuex.Store({
  state: {
    city: '北京'
  },
  actions: {
    changeCity (ctx, city) { // ctx为上下文
      ctx.commit('changeCity', city)
    }
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
    }
  }
})
可以跳过acitions
methods: {
    handleCityClick (city) {
      this.$store.commit('changeCity', city)
    }
  }
export default new Vuex.Store({
  state: {
    city: '北京'
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
    }
  }
})

点击城市返回主页
vue官网-生态系统-vue router-编程式导航
methods: {
    handleCityClick (city) {
      this.$store.commit('changeCity', city)
      this.$router.push('/')
    }
  }

#vuex的高级使用及localStorage
刷新后选择的城市不变
export default new Vuex.Store({
  state: {
    city: localStorage.city || '北京'
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
      localStorage.city = city
    }
  }
})
使用localStorage建议使用try catch
let defaultCity = '北京'
try {
    if (localStorage.city) {
        defaultCity =  localStorage.city = city
    }
} catch (e) {}
export default new Vuex.Store({
  state: {
    city: defaultCity
  },
  mutations: {
    changeCity (state, city) {
      state.city = city
      try {
        localStorage.city = city
      } catch (e) {}
    }
  }
})
把state和mutation提取出来分别创建js
城市名称过长,布局错误修复
width改为min-width: 1.04rem

优化this.$store.state.city过长
#关于mapState
this.city
<script>
import { mapState } from 'vuex'
export default{
  computed: {
    ...mapState(['city'])
  }
}
</script>
另一种写法
<script>
import { mapState } from 'vuex'
this.currentCity
 computed: {
    ...mapState({
      currentCity: 'city'
    })
  }
</script>
Mutations优化
#关于mapMutations
import { mapState, mapMutations } from 'vuex'
 methods: {
    handleCityClick (city) {
      // this.$store.commit('changeCity', city)
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  }
#关于mapGetters 
(类似与compued的作用)
export default new Vuex.Store({
  getters: {
    doubleCity (state) {
        return state.city + ' ' + state.city
        }
    }
}
 computed: {
    ...mapGetters(['doubleCity'])
  }
import { mapGetters } from 'vuex'
{{this.doubleCity}}

#关于Module
将代码按照模块拆分

#keepalive优化
chrome/Network/xhs可以查看json请求次数
切换页面时,请求json,再切换.再次请求一样的json,由于每次页面的mounted重复执行
修改App.vue
<template>
  <div id="app">
    <keep-alive>
        <router-view/> 
    </keep-alive>
  </div>
</template>
修改城市时,应该重新获取ajax请求
在home.vue修改
import { mapState } from 'vuex'
axios.get('/api/index.json?city' + this.city).then(this.getHomeInfoSucc)
computed: {
    ...mapState(['city'])
  },
在chrome/Network/xhs/index.json/headers能找到city北京,此时点击按钮,不会重新发ajax请求
使用keepalive会多出来个生命周期函数activated
此时mounted不会重复执行
但是activated会重复执行(页面被重新显示的时候被执行)
lastCity: ''
mounted () {
    this.getHomeInfo()
    this.lastCity = this.city
  }
activated () {
if (this.lastCity !== this.city) {
  this.lastCity = this.city
  this.getHomeInfo()
}
}
#详情页面动态路由及banner布局
<router-link :to='./detail/ +"item.id"'><li></li></router-link>
颜色修复方法
</router-link>
index.js添加路由
{
    path: '/detail/:id',//传的值给id
    name: 'Detail',
    component: Detail
  }
  background-image: linear-gradient(top, rgba(0, 0, 0, 0),rgba(0, 0, 0, .8))渐变色
#公共图片画廊组件拆分
创建 src/common/gallery/Gallery.vue
创建common目录简写
swiperOption的选项
https://3.swiper.com.cn/plus/search.php?kwtype=0&q=pagination
修复轮播图0/0
observeParents: true,
observer: true

#header渐隐渐现的效果
<div class="content"></div>
.content
height: 50rem//页面较长,用于撑开页面,以便调试
监听window.onscroll
    window.addEventListener('scroll',this.handleScroll)
console.log(document.documentElement.scrollTop)
:style='opacityStyle'
handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) { // 60-140渐隐渐现
        let opacity = top / 140
        opacity = opacity > 1 ?  1: opacity
        this.opacityStyle = { opacity }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
#全局事件解绑
windows.addEventListen添加到了全局,
返回主页面也会有事件监听
所以需要解绑
keep-alive的使用会多生命周期函数activated还有deactivated
在deactivated里取消监听即可
    window.removeEventListener('scroll', this.handleScroll)
#使用递归组件实现详情页列表
子组件中name的作用是使用递归组件
<div v-if='item.children'>
    <detail-list :list='item.children'></detail-list>
</div>
可以一直递归到完 
#detail页面ajax请求
getDetailInfo: function () {
      axios.get('/api/detail.json?id=' + this.$route.params.id).then(this.getDetailInfoSucc)
    },
或
 getDetailInfo: function () {
      axios.get('/api/detail.json?id=', {
        params: {
            id: this.$route.params.id
        }
      }).then(this.getDetailInfoSucc)
    }
props里判断类型
换页时由于keeplive不会重新请求
可以用activated修复
或
在App.vue里修改
<template>
  <div id="app">
    <keep-alive exclude='Detail'>
        <router-view/>
    </keep-alive>
  </div>
</template>
这样Detail不会被缓存

name作用总结
1.递归组件使用
2.不让组件缓存时使用
3.Vue的开发工具里组件名的来源

修复首页拖动到某一位置,其他页面也会被拖到相应位置
官网vue/vue-router/滚动行为
  scrollBehavior (to, from, savedPosition) {
    return { x: 0, y: 0 }
  }
#创建动画
common下创建fade/Fade.vue
内容详见learnLog3.txt