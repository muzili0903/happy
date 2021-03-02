<template>
  <div class="list" ref="wraaper">
    <div>
      <div class="area">
        <!-- border-topbottom 1像素边框 -->
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{this.currentCity}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div class="button-wrapper" v-for="item of hot" :key="item.id" @click="handleCityClick(item.name)">
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div class="area" v-for="(item, key) of cities" :key="key"
           :ref="key">
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list">
          <div class="item border-bottom" v-for="innerItem of item" :key="innerItem.id"
               @click="handleCityClick(innerItem.name)">{{innerItem.name}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'CityList',
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  computed: {
    ...mapState({
      // 把 vuex 中的 city 映射到 computed 属性中，名字为 currentCity
      currentCity: 'city'
    })
  },
  methods: {
    handleCityClick (city) {
      // 调用 vuex 中的 Actions 需要先调用 dispatch
      // 非批量数据可以省略调用 actions 可以直接调用commit
      // this.$store.dispatch('changeCity', city)
      // this.$store.commit('changeCity', city)
      this.changeCity(city)
      this.$router.push('/')
    },
    // 把 vuex 中 Mutations 的 changeCity 映射到这个组件中，名字叫做 changeCity
    ...mapMutations(['changeCity'])
  },
  // 监听器
  watch: {
    cities () {
      this.$nextTick(() => {
        this.scroll.refresh()
      })
    },
    letter () {
      if (this.letter) {
        // this.$refs[this.letter] 获取到的是一个数组
        const element = this.$refs[this.letter][0]
        // scrollToElement 必须传送一个元素
        this.scroll.scrollToElement(element)
      }
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wraaper)
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  // 把 border-topbottom 对应的边框颜色变成 #ccc
  .border-topbottom
    &:before
      border-color #ccc
    &:after
      border-color #ccc

  .border-bottom
    &:before
      border-color #ccc

  .list
    // 超出部分隐藏
    overflow hidden
    position absolute
    top 1.58rem
    left 0
    right 0
    bottom 0
    .title
      line-height .54rem
      background #eee
      padding-left .2rem
      color #666
      font-size .26rem
    .button-list
      overflow hidden
      // 上 右 下 左
      padding .1rem .6rem .1rem .1rem
      .button-wrapper
        // 用到 float 时，父级需要加上 overflow hidden
        float left
        width 33.33%
        .button
          margin .1rem
          padding .1rem 0
          text-align center
          // 不用 1像素边框 用 border .02rem solid #ccc
          border .02rem solid #ccc
          border-radius .06rem
    .item-list
      .item
        line-height .76rem
        padding-left .2rem
</style>
