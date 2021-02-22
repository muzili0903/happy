<template>
    <div class="list">
      <ul>
        <li class="item" v-for="(item, key) of cities" :key="key">{{key}}</li>
      </ul>
    </div>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  .list
    // 垂直方向上居中 {
    display flex
    flex-direction column
    justify-content center
    // 垂直方向上居中 }
    position absolute
    top 1.58rem
    right 0
    bottom 0
    width .4rem
    .item
      // 设置高度
      line-height .4rem
      text-align center
      color $bgColor
</style>
