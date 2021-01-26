<template>
  <div class="wrapper">
    <swiper :options="swiperOptions">
      <swiper-slide v-for="item of swiperList" :key=item.id>
        <img class="swiper-img" :src="item.imgeUrl"/>
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  data () {
    return {
      swiperOptions: {
        pagination: '.swiper-pagination',
        // 轮播可以循环轮播
        loop: true
      },
      swiperList: [{
        id: '0001',
        imgeUrl: 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=68285350,561487286&fm=26&gp=0.jpg'
      },
      {
        id: '0002',
        imgeUrl: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=2353279619,1248476231&fm=26&gp=0.jpg'
      }]
    }
  }
}
</script>

<style lang="stylus" scoped>
  // wrapper 所有子组件的 swiper-pagination-bullet-active 都变成白色
  .wrapper >>> .swiper-pagination-bullet-active
    background : #fff
  .wrapper
    overflow: hidden
    width: 100%
    height: 0
    padding-bottom: 31.25%
    .swiper-img
      width: 100%
</style>
