<template>
    <div class="search">
        <input type="text" placeholder="输入城市名或拼音" class="search-input">
    </div>
</template>

<script>
export default {
  name: 'CitySearch'
}
</script>

<style lang='stylus' scoped>
 @import '~styles/varibles.styl'
 .search
     height: .72rem
     background: $bgcolor
     padding: 0 .1rem
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
         margin-top: .05rem
</style>
