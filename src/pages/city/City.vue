<template>
    <div>
        <city-header></city-header>
        <city-search :cities='cities'></city-search>
        <city-list :cities="cities" :hot="hotCities" :letter='letter'></city-list>
        <city-alphabet :cities='cities' @change='handelLetterChange'></city-alphabet>
    </div>
</template>

<script>
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
import axios from 'axios'
export default {
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  mounted () {
    this.getCityInfo()
  },
  methods: {
    getCityInfo: function () {
      axios.get('/api/city.json').then(this.getCityInfoSucc)
    },
    getCityInfoSucc: function (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    handelLetterChange: function (letter) {
      this.letter = letter
    }
  }
}
</script>

<style lang='stylus' scoped>

</style>
