<template>
  <div>
    <div class="recommend-title">热门推销</div>
    <ul>
      <!-- li 引入 1像素边框 border-bottom-->
      <router-link tag="li"
                   class="item border-bottom"
                   v-for="item of list" :key="item.id"
                   :to="'/detail/' + item.id">
        <img class="item-img" :src="item.imgUrl"/>
        <div class="item-info">
          <p class="item-title">{{item.title}}</p>
          <p class="item-desc">{{item.desc}}</p>
          <button class="item-button">查看详情</button>
        </div>
      </router-link>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HomeRecommend',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/mixins.styl"
  .recommend-title
    margin-top .2rem
    line-height .8rem
    background #eee
    text-indent .2rem

  .item
    overflow hidden
    display flex
    height 1.9rem
    .item-img
      // 图片定宽定高
      width 1.7rem
      height 1.7rem
      // 上下左右都是 .1rem
      padding .1rem
    .item-info
      // flex 1 自动撑开屏幕的宽度
      flex 1
      padding .1rem
      // ellipsis() 没有显示 ... 需要加上 min-width 0
      min-width 0
      .item-title
        line-height .54rem
        font-size .32rem
        ellipsis()
      .item-desc
        line-height .4rem
        color #ccc
        ellipsis()
      .item-button
        // 调整 button 的高度
        line-height .44rem
        margin-top .16rem
        background #ff9300
        // 上下 0rem 左右 .2rem
        padding 0 .2rem
        // 给border 一个圆角
        border-radius .06rem
        color #fff
</style>
