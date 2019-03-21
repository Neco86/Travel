<template>
    <div>
        <detail-banner></detail-banner>
        <detail-header></detail-header>
        <div class="content">
             <detail-list :list='list'></detail-list>
        </div>
    </div>
</template>

<script>
import DetailBanner from './components/Banner'
import DetailHeader from './components/Header'
import DetailList from './components/List'
export default{
  name: 'Detail',
  components: {
    DetailBanner,
    DetailHeader,
    DetailList
  },
  data () {
    return {
      list: [{
        title: '成人票',
        children: [{
          title: '一票全含',
          children: [{title: '一票全含-上午场'}]
        }, {
          title: '贺岁迎新'
        }]
      }, {
        title: '学生票'
      }, {
        title: '儿童票'
      }, {
        title: '特惠票'
      }
      ]
    }
  }
}
</script>

<style lang='stylus' scoped>
    .content
        height: 50rem//页面较长,用于撑开页面
</style>
