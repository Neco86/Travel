<template>
    <div>
        <div class="banner" @click='handleBannerClick'>
            <img src="http://img1.qunarzz.com/sight/p0/1409/19/adca619faaab0898245dc4ec482b5722.jpg_600x330_f922b488.jpg" class="banner-img">
            <div class="banner-info">
                <div class="banner-title">故宫(AAAAA景区)</div>
                <div class="banner-number"><span class="iconfont banner-iconfont">&#xe60f;</span>8</div>
            </div>
        </div>
        <common-gallery :imgs='imgs' v-show='showGallery' @close='handleGalleryClose'></common-gallery>
    </div>
</template>

<script>
import CommonGallery from 'common/gallery/Gallery'
export default{
  name: 'Banner',
  data () {
    return {
      showGallery: false,
      imgs: ['http://img1.qunarzz.com/sight/p0/1409/19/adca619faaab0898245dc4ec482b5722.jpg_r_800x800_6edd8174.jpg', 'http://img1.qunarzz.com/sight/p55/201211/04/fbcab3e5d6479ce893835fbb.jpg_r_800x800_6360f514.jpg', 'http://img1.qunarzz.com/wugc/p180/201306/16/7f08e81624346b1693835fbb.jpg_r_800x800_5f03ad73.jpg']
    }
  },
  components: {
    CommonGallery
  },
  methods: {
    handleBannerClick () {
      this.showGallery = true
    },
    handleGalleryClose () {
      this.showGallery = false
    }
  }
}
</script>

<style lang='stylus' scoped>
    .banner
        position: relative
        overflow: hidden
        height: 0
        padding-bottom: 55%
        .banner-img
            width: 100%
        .banner-info
            position: absolute
            left: 0
            right: 0
            bottom: 0
            line-height: .6rem
            display: flex
            color: #fff
            background-image: linear-gradient(top, rgba(0, 0, 0, 0),rgba(0, 0, 0, .8))
            .banner-title
                flex: 1
                font-size: .32rem
                padding: 0 .2rem
            .banner-number
                margin-top: .14rem
                padding: 0 .25rem
                line-height: .32rem
                height: .32rem
                border-radius: .2rem
                background: rgba(0, 0, 0,.8)
                font-size: .24rem
                margin-right: .2rem
                .banner-iconfont
                    font-size: .24rem
                    margin-right: .1rem
</style>
