<template>
  <div class="icons">
    <swiper>
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
  data () {
    return {
      iconList: [{
        id: '001',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '002',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/flight.png',
        imgDesc: '机票'
      }, {
        id: '003',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '火车票'
      }, {
        id: '004',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/flight.png',
        imgDesc: '度假'
      }, {
        id: '005',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '景点门票'
      }, {
        id: '006',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '007',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/flight.png',
        imgDesc: '机票'
      }, {
        id: '008',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/flight.png',
        imgDesc: '火车票'
      }, {
        id: '009',
        imgUrl: '//s.qunarzz.com/homenode/images/touchheader/flight.png',
        imgDesc: '火车票'
      }]
    }
  },
  // 计算属性用来实现分页效果
  computed: {
    pages () {
      const pages = []
      this.iconList.forEach((item, index) => {
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
  .icons >>> .swiper-container
    height 0
    padding-bottom 50%
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
