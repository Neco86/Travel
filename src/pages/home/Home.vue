<template>
    <div>
        <home-header></home-header>
        <home-swiper :list='swiperList'></home-swiper>
        <home-icons :list='iconList'></home-icons>
        <home-recommend :list='recommendList'></home-recommend>
        <home-weekend :list='weekendList'></home-weekend>
    </div>
</template>

<script>
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weekend'
import axios from 'axios'
import { mapState } from 'vuex'
export default{
  name: 'Home',
  components: {
    HomeHeader: () => import('./components/Header'),
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend
  },
  data () {
    return {
      swiperList: [],
      iconList: [],
      recommendList: [],
      weekendList: [],
      lastCity: ''
    }
  },
  computed: {
    ...mapState(['city'])
  },
  mounted () {
    this.getHomeInfo()
    this.lastCity = this.city
  },
  methods: {
    getHomeInfo: function () {
      axios.get('/api/index.json?city' + this.city).then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc: function (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.swiperList = data.swiperList
        this.iconList = data.iconList
        this.recommendList = data.recommendList
        this.weekendList = data.weekendList
      }
    }
  },
  activated () {
    if (this.lastCity !== this.city) {
      this.lastCity = this.city
      this.getHomeInfo()
    }
  }
}
</script>

<style>

</style>
