<template>
  <div>
    <div class="search">
      <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音"/>
    </div>
    <div class="search-content" ref="search" v-show="keyword">
      <ul>
        <li class="search-item border-bottom" v-for="item of list" :key="item.id" @click="handleCityClick(item.name)">
          {{item.name}}
        </li>
        <li class="search-item border-bottom" v-show="hasNoData">没有匹配到内容</li>
      </ul>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'

export default {
  name: 'citySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      timer: null,
      list: []
    }
  },
  methods: {
    handleCityClick (city) {
      // 调用 vuex 中的 Actions 需要先调用 dispatch
      // 非批量数据可以省略调用 actions 可以直接调用commit
      // this.$store.dispatch('changeCity', city)
      // this.$store.commit('changeCity', city)
      this.changeCity(city)
      // 点击城市跳转到首页
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 ||
              value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    },
    list () {
      this.$nextTick(() => {
        this.scroll.refresh()
      })
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.search)
    console.log(this.scroll)
  },
  computed: {
    hasNoData () {
      return !this.list.length
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  .search
    height .72rem
    padding 0 .1rem
    background $bgColor
    .search-input
      width 100%
      box-sizing border-box
      padding 0 .1rem
      height .62rem
      line-height .62rem
      text-align center
      border-radius .06rem
      color #666

  .search-content
    // z-index 页面全部显示
    z-index 1
    overflow hidden
    position absolute
    background #eaeaea
    top 1.58rem
    left 0
    right 0
    bottom 0
    .search-item
      line-height .62rem
      padding-left .2rem
      background #ffffff
      color #666
</style>
