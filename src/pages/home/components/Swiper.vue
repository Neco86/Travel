<template>
    <div class="wrapper">
        <swiper :options="swiperOption" v-if='showSwiper'>
        <swiper-slide v-for='item of list' :key='item.id'>
            <img :src="item.imgUrl" class="swiper-img">
        </swiper-slide>
        <div class="swiper-pagination"  slot="pagination"></div>
      </swiper>
    </div>
</template>

<script>
export default{
  name: 'HomeSwiper',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true,
        autoplay: 5000
      }
    }
  },
  computed: {
    showSwiper () {
      return this.list.length
    }
  }
}
</script>

<style lang="stylus" scoped>
    .wrapper >>> .swiper-pagination-bullet-active
        background-color: #fff
    .wrapper
        width: 100%
        height: 0
        overflow: hidden
        padding-bottom: 25.6%
        background-color: #eee;
        .swiper-img
            width: 100%
</style>
