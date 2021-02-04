<template>
  <div class="icons">
    <swiper :options="swiperOptions">
      <swiper-slide v-for="(page, index) of pages" :key="index">
        <div class="icon" v-for="item of page" :key="item.id">
          <div class="icon-img">
            <img class="icon-imgContent" :src="item.imgUrl"/>
          </div>
          <p class="icon-desc">{{item.imgDesc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOptions: {
        // 控制 轮播图不要自动滚动
        autoplay: false
      }
    }
  },
  // 计算属性用来实现分页效果
  computed: {
    pages () {
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
  // 引入varibles.sytl下的常量
  @import '~styles/varibles.styl'
  @import "~styles/mixins.styl"
  // icons所处的 div 能够滑动
  .icons >>> .swiper-container
    height 0
    padding-bottom 50%
  .icons
    margin-top .1rem
    .icon
      position relative
      overflow hidden
      float left
      width 25%
      height 0
      padding-bottom 25%
      .icon-img
        // absolute 相当于根元素的 absolute，需要在icon中加上 position relative
        position absolute
        top 0
        left 0
        right 0
        bottom .44rem
        // 图片有一个5像素的间距 box-sizing border-box padding .1rem
        box-sizing border-box
        padding .1rem
        .icon-imgContent
          // 图片自动居中 display block margin 0 auto
          display block
          margin 0 auto
          height 100%
      .icon-desc
        position absolute
        left 0
        right 0
        bottom 0
        height .44rem
        line-height .44rem
        text-align center
        color $darkTextColor
        // 实现字体显示不全用 ...代替的代码 overflow hidden white-space nowrap text-overflow ellipsis
        ellipsis()
</style>
