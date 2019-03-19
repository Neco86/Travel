<template>
    <ul class="list">
        <li
        class="item"
        v-for='item of letters'
        :key='item'
        @click='handleLeterClick'
        @touchstart='handleTouchStart'
        @touchmove='handleTouchMove'
        @touchend='handleTouchEnd'
        :ref='item'
        >{{item}}</li>
    </ul>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop// A距离顶部距离,优化:放到updated里而不是每次计算
  },
  methods: {
    handleLeterClick (e) {
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.timmer) {
        clearTimeout(this.timer)
      }
      this.timer = setTimeout(() => { // 函数节流,减少函数执行次数,实现性能优化
        if (this.touchStatus) {
          const touchY = e.touches[0].clientY - 79.5// 手指滑动位置距离顶部位置
          const index = Math.floor((touchY - this.startY) / 20) // 计算是哪个字母
          if (index >= 0 && index < this.letters.length) {
            this.$emit('change', this.letters[index])
          }
        }
      }, 16)
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
  }
}
</script>

<style lang='stylus' scoped>
  @import '~styles/varibles.styl'
  .list
      display: flex
      flex-direction: column
      justify-content: center
      position: absolute
      right: 0
      top: 1.58rem
      bottom: 0
      width: .44rem
      .item
          line-height: .4rem
          text-align: center
          color: $bgcolor
</style>
