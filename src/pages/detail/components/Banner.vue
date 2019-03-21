<template>
    <div>
        <div class="banner" @click='handleBannerClick'>
            <img :src="bannerImg">
            <div class="banner-info">
                <div class="banner-title">{{this.sightName}}</div>
                <div class="banner-number"><span class="iconfont banner-iconfont">&#xe60f;</span>{{this.bannerImgs.length}}</div>
            </div>
        </div>
        <common-gallery :imgs='bannerImgs' v-show='showGallery' @close='handleGalleryClose'></common-gallery>
    </div>
</template>

<script>
import CommonGallery from 'common/gallery/Gallery'
export default{
  name: 'Banner',
  data () {
    return {
      showGallery: false
    }
  },
  props: {
    sightName: String,
    bannerImg: String,
    bannerImgs: Array
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
