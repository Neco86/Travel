<template>
    <div class="container" @click='handleGalleryClick'>
        <div class="wrapper">
            <swiper :options="swiperOption">
                <swiper-slide v-for='(item,index) in imgs' :key='index'><img :src='item' class="gallery-img"></swiper-slide>
                <div class="swiper-pagination"  slot="pagination"></div>
             </swiper>
        </div>
    </div>
</template>

<script>
export default {
  name: 'CommonGallery',
  props: {
    imgs: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: false,
        autoplay: false,
        paginationType: 'fraction',
        observeParents: true,
        observer: true
      }
    }
  },
  methods: {
    handleGalleryClick () {
      this.$emit('close')
    }
  }
}
</script>

<style lang='stylus' scoped>
    .container >>> .swiper-container{
        overflow: inherit
    }
    .container
        display: flex
        flex-direction: column
        justify-content: center
        position: fixed
        left: 0
        right: 0
        top: 0
        bottom: 0
        background: #000
        z-index: 99
        .wrapper
            width: 100%
            height: 0
            padding-bottom: 100%
            .gallery-img
                width: 100%
            .swiper-pagination
                color: #fff
                bottom: -1rem
</style>
