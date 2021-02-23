<template>
  <!-- 监听滑动的三个函数 touchstart touchmove touchend -->
  <div class="list">
    <ul>
      <li class="item" v-for="item of letters"
          :key="item"
          :ref="item"
          @click="handleLetterClick"
          @touchstart="handleTouchStart"
          @touchmove="handleTouchMove"
          @touchend="handleTouchEnd">{{item}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'CityAlphabet',
  props: {
    cities: Object
  },
  // 通过计算属性获取城市首字母
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  data () {
    return {
      touchStatus: false,
      startY: 0,
      timer: null
    }
  },
  // 当页面数据被更新时，执行该勾子函数
  updated () {
    // 获取第一个元素到顶部的高度
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    handleLetterClick (e) {
      // 获取点击内容 并传输给父组件 父组件监听 change 事件
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    // 手指在页面上下滑动的时候，此函数被执行
    handleTouchMove (e) {
      if (this.touchStatus) {
        // 做数据节流，提高网页性能
        if (this.timer) {
          clearTimeout(this.timer)
        }
        // 延时 16ms 做手指滚动这件事
        this.timer = setTimeout(() => {
          // 获取手指点击位置到顶部的高度
          const touchY = e.touches[0].clientY - 79
          // 获取每个字母的下标 = 手指位置高度 - 第一个元素位置高度 除于 字母高度
          const index = Math.floor((touchY - this.startY) / 20)
          if (index >= 0 && index < this.letters.length) {
            // 获取字母并传送给父组件
            this.$emit('change', this.letters[index])
          }
        }, 16)
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    }
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
