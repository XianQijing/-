<template>
  <div id="app">
    <v-header :seller='seller'/>
    <div class="tab border-bottom">
      <div class="tab-item">
        <router-link :to="{ path: '/goods' }">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ path: '/ratings' }">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ path: '/seller' }">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"/>
  </div>
</template>

<script>
import Header from './components/header/header'

const ERR_OK = 0

export default{
  name: 'App',
  data () {
    return {
      seller: {}
    }
  },
  components: {
    'v-header': Header
  },
  created () {
    this.$axios.get('/api/seller').then(res => {
      if (res.data.errno === ERR_OK) {
        this.seller = res.data.data
      }
    })
  }
}
</script>

<style lang="stylus" scoped>
@import './common/stylus/mixin.styl';
#app
  .tab
    display flex
    width 100%
    height 40px
    line-height 40px
    .tab-item
      flex 1
      text-align center
      & > a
        display block
        font-size 14px
        color rgb(77, 85 93)
      .router-link-active
        color red
</style>
