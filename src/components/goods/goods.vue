<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" :key="item.name" class="meun-item">
          <span class="text border-bottom">
            <span v-show="item.type > 0" class="icon" :class="classMap[item.type]"></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      <ul>
        <li v-for="item in goods" :key="item.foods.name">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" :key="food.name" class="food-item">
              <div class="icon">
                <img :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'goods',
  data () {
    return {
      goods: {}
    }
  },
  created () {
    this.classMap = ['decrease', 'special', 'discount', 'invoice', 'guarantee']
    this.$axios.get('/api/goods').then(res => {
      this.goods = res.data.data
    })
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mixin.styl';
.goods
  position absolute
  top 174px
  bottom 64px
  display flex
  width 100%
  overflow hidden
  .menu-wrapper
    flex 0 0 80px
    width 80px
    background #f3f5f7
    .meun-item
      display table
      height 54px
      width 56px
      line-height 14px
      padding 0 12px
      .icon
        display inline-block
        width 12px
        height 12px
        margin-right 2px
        background-size 12px 12px
        background-repeat no-repeat
        vertical-align top
        &.decrease
          bg-image('decrease_3')
        &.discount
          bg-image('discount_3')
        &.guarantee
          bg-image('guarantee_3')
        &.invoice
          bg-image('invoice_3')
        &.special
          bg-image('special_3')
      .text
        font-size 10px
        line-height 12px
        display table-cell
        vertical-align middle
  .foods-wrapper
    flex 1
</style>
