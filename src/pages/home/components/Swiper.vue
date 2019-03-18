<template>
    <div class="wrapper">
        <swiper :options="swiperOption">
        <swiper-slide v-for='item of swiperList' :key='item.id'>
            <img :src="item.imgUrl" class="swiper-img">
        </swiper-slide>
        <div class="swiper-pagination"  slot="pagination"></div>
      </swiper>
    </div>
</template>

<script>
export default{
  name: 'HomeSwiper',
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      },
      swiperList: [{
        id: '0001',
        imgUrl: 'https://source.qunarzz.com/site/images/wns/20190222_qunar_dujia_homepage_3.jpg'
      }, {
        id: '0002',
        imgUrl: 'https://source.qunarzz.com/site/images/wns/20190313_dujia_homepage_top_banner_5.jpg'
      }]
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
