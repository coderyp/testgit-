<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  data () {
    return {
      bs: null
    }
  },
  props: {
      probeType: {
        type: Number,
        default: 0
      },
      pullUpLoad: {
        type: Boolean,
        default: false
      }
  },
  mounted () {
    this.bs = new BScroll(this.$refs.wrapper, {
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad,
      click: true
    })
    // 监听滚动的位置
    this.bs.on('scroll', (position) => this.$emit('scroll', position))
    // 监听上拉事件
    this.bs.on('pullingUp', () => {
      console.log('上垃加载更多')
      this.$emit('loadMore')
      setTimeout( () => {
        this.bs.finishPullUp()
      }, 1000)
    })
  },
  methods: {
    scrollTo (x, y, time = 300) {
      this.scroll && this.bs.scrollTo(x, y, time)
    },
    // 封装refresh方法
    refresh () {
      this.scroll && this.bs.refresh()
    }
  }
}
</script>

<style>
  .wrapper {
    overflow: hidden;
  }
</style>