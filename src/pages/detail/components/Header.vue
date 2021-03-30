<template>
  <div>
    <router-link tag="div" to="/" class="header-abs" v-show="showAbs">
      <div class="iconfont header-abs-back">&#xe624;</div>
    </router-link>
    <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
      景点详情
      <router-link to="/">
        <div class="iconfont header-fixed-back">&#xe624;</div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: 0
    }
  },
  methods: {
    // 渐隐渐显的动画效果
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) {
        this.showAbs = false
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = {opacity}
      } else {
        this.showAbs = true
      }
    }
  },
  // 因为用了keepalive 所以页面只要被展示，activated 就会被执行
  activated () {
    // 监听 scroll 事件
    window.addEventListener('scroll', this.handleScroll)
  },
  // 因为用了 keepalive 所以页面只要被关闭，deactivated 就会被执行
  deactivated () {
    // 全局事件需要解绑，避免出现 bug
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  .header-abs
    position absolute
    left .2rem
    top .2rem
    width .8rem
    height .8rem
    line-height .8rem
    text-align center
    border-radius .4rem
    background rgba(0, 0, 0, .8)
    .header-abs-back
      color #ffffff
      font-size .4rem

  .header-fixed
    z-index 2
    position fixed
    top 0
    left 0
    right 0
    height $headerHeight
    line-height $headerHeight
    text-align center
    color #fff
    background $bgColor
    font-size .32rem
    .header-fixed-back
      position absolute
      top 0
      left 0
      width .64rem
      text-align center
      font-size .4rem
      color #ffffff
</style>
