<template>
  <div>
    <div class="item" v-for="(item, index) of list" :key="index">
      <div class="item-title border-bottom">
        <span class="item-title-icon"></span>
        {{item.title}}
      </div>
      <!-- 递归组件的使用-->
      <div class="item-children" v-if="item.children">
        <detail-list :list="item.children"></detail-list>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailList',
  props: {
    list: Array
  }
}
</script>

<style lang="stylus" scoped>
  .item-title
    line-height .8rem
    font-size .32rem
    padding 0 .2rem
    .item-title-icon
      position relative
      left .06rem
      top .06rem
      display inline-block
      width .36rem
      height .36rem
      background url("//bpic.588ku.com/element_pic/20/06/30/8acc972efee121b6b7150048251b5a8f.jpg!/fw/253/quality/90/unsharp/true/compress/true") 0 -.45rem no-repeat
      margin-right .1rem
      background-size .4rem 3rem
  .item-children
    padding 0 .2rem
</style>
