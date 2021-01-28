<template>
  <div>
    <div class="title">周末去哪儿</div>
    <ul>
      <li v-for="item of weekendList" :key="item.id">
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
  data () {
    return {
      weekendList: [{
        id: '001',
        imgUrl: 'https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=4161958695,1981548690&fm=15&gp=0.jpg',
        title: '大连圣亚海洋世界',
        desc: '浪漫大连首战，浪漫的海洋主题乐园'
      }, {
        id: '002',
        imgUrl: 'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimage.photophoto.cn%2Fnm-23%2F036%2F003%2F0360030791.jpg&refer=http%3A%2F%2Fimage.photophoto.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1614432597&t=d8b0d37b63d4d81b0a1d4f5102ffb704',
        title: '大连圣亚海洋世界',
        desc: '浪漫大连首战，浪漫的海洋主题乐园'
      }]
    }
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
