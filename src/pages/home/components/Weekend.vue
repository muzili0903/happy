<template>
  <div>
    <div class="title">周末去哪儿</div>
    <ul>
      <li v-for="item of list" :key="item.id">
        <div class="weekend-img-wrapper">
          <img class="weekend-img" :src="item.imgUrl"/>
        </div>
        <div class="weekend-info">
          <p class="weekend-title">{{item.title}}</p>
          <p class="weekend-desc">{{item.desc}}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HomeWeekend',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/mixins.styl"
  .title
    margin-top .2rem
    line-height .8rem
    background #eee
    text-indent .2rem
  .weekend-img-wrapper
    overflow hidden
    height 0
    padding-bottom 33.9%
    .weekend-img
      width 100%
  .weekend-info
    padding 0.1rem
    .weekend-title
      line-height .54rem
      font-size .32rem
      ellipsis()
    .weekend-desc
      line-height .54rem
      font-size .32rem
      color #ccc
      ellipsis()
</style>
