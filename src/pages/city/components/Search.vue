<template>
    <div>
         <div class="search">
            <input type="text" placeholder="输入城市名或拼音" class="search-input" v-model="keyword">
        </div>
        <div class="search-content" ref='search' v-show='keyword'>
            <ul>
                <li v-for='item of list' class="search-item  border-bottom" :key='item.id' @click='handleCityClick(item.name)'>{{item.name}}</li>
                <li class="search-item  border-bottom" v-show='hasNoData'>没有找到匹配数据</li>
            </ul>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timmer: null
    }
  },
  computed: {
    hasNoData () {
      return !this.list.length
    }
  },
  watch: {
    keyword () {
      if (this.timmer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => { // 函数节流,减少函数执行次数,实现性能优化
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  methods: {
    handleCityClick (city) {
      // this.$store.commit('changeCity', city)
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.search)
  }
}
</script>

<style lang='stylus' scoped>
 @import '~styles/varibles.styl'
 .search
     height: .72rem
     background: $bgcolor
     padding: 0 .1rem
     padding-bottom: 0.01rem
     margin-top: -0.02rem
     .search-input
         height: .62rem
         line-height: .62rem
         width: 100%
         text-align: center
         border-radius: .06rem
         color: #666
         box-sizing: border-box
         padding: 0 .1rem
         margin-top: .025rem
 .search-content
     position: absolute
     top: 1.58rem
     left: 0
     right: 0
     bottom: 0
     overflow: hidden
     background: #eee
     z-index: 1
     .search-item
         line-height: .62rem
         padding-left: .2rem
         color: #666
         background: #fff
</style>
