<template>
    <div>
      <detail-banner></detail-banner>
      <detail-header></detail-header>
      <!--为了让页面可以滚动，添加 div -->
      <div class="content"></div>
    </div>
</template>

<script>
import DetailBanner from './components/Banner'
import DetailHeader from './components/Header'
export default {
  name: 'Detail',
  components: {
    DetailBanner,
    DetailHeader
  }
}
</script>

<style lang="stylus" scoped>
  .content
    height 50rem
</style>
