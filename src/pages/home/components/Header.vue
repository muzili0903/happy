<template>
  <div class="header">
    <div class="header-left">
      <div class="iconfont back-icon">&#xe624;</div>
    </div>
    <div class="header-input">
      <span class="iconfont">&#xe632;</span>
      输入城市/景点/游玩主题
    </div>
    <!-- router-link 路由跳转 跳转到 /city 路径-->
    <router-link to="city">
      <div class="header-right">
        {{this.city}}
        <span class="iconfont arrow-icon">&#xe6aa;</span>
      </div>
    </router-link>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex'

export default {
  name: 'HomeHeader',
  computed: {
    // ... 展开运算符
    // mapState 把 vuex 中的 city 映射到 computed 中
    ...mapState(['city']),
    ...mapGetters(['doubleCity'])
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  @import "~styles/mixins.styl"
  .header
    display flex
    line-height: $headerHeight
    background: $bgColor
    color: #fff
    .header-left
      width: .64rem
      float: left
      .back-icon
        text-align: center
        font-size: .4rem
    .header-right
      // 如果写成 width 1.04 宽度就写死了
      // 写成 min-width 根据内容展示宽度，最少宽度 1.04
      min-width 1.04rem
      padding 0 .1rem
      float: right
      text-align: center
      color #ffffff
      .arrow-icon
        font-size: .24rem
        margin-left: -.04rem
    .header-input
      flex: 1
      background: #fff
      border-radius: .1rem
      margin-top: .12rem
      height: .64rem
      line-height: .64rem
      margin-left: .2rem
      padding-left: .1rem
      color: #ccc
</style>
