<template>
    <div>
        <router-link tag='div' to='/' class="header-abs" v-show='showAbs'>
            <div class="iconfont header-abs-back">&#xe624;</div>
        </router-link>
        <div class="header-fixed" v-show='!showAbs' :style='opacityStyle'>
            <router-link to='/'>
                <div class="iconfont header-fixed-back">&#xe624;</div>
             </router-link>
             景点详情
        </div>
    </div>
</template>

<script>
export default{
  name: 'Header',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  mounted () {
    window.addEventListener('scroll', this.handleScroll)
  },
  unmounted () {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) { // 60-140渐隐渐现
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = { opacity }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  }

}
</script>

<style lang='stylus' scoped>
    @import '~styles/varibles.styl'
    .header-abs
        position: absolute
        left: .2rem
        top: .2rem
        width: .8rem
        height: .8rem
        border-radius: .4rem
        background: rgba(0, 0, 0, .8)
        text-align: center
        line-height: .8rem
        .header-abs-back
            color: #fff
            font-size: .4rem
    .header-fixed
         position: fixed
         top: 0
         left: 0
         right: 0
         height: $headerHeight
         line-height: $headerHeight
         text-align: center
         color: #fff
         background-color: $bgcolor
         font-size: .32rem
         z-index: 2
         .header-fixed-back
             position: absolute
             width: .64rem
             text-align: center
             font-size: .4rem
             top: 0
             left: 0
             color: #fff
</style>
