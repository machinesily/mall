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
    data() {
      return {
        scroll: null
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
    mounted() {
      this.scroll = new BScroll(this.$refs.wrapper, {
          observeDOM: true, //不加这个不滚动
          click: true,
          probeType: this.probeType,
          pullUpLoad: this.pullUpLoad
        })

        this.scroll.on('scroll', position => {
          this.$emit('scrollPosition', position)
        })

        if(this.pullUpLoad) {
          this.scroll.on('pullingUp', () => {
            this.$emit('pullingUp')
          })
        }
    },
    methods: {
      scrollTo(x, y, time = 1000) {
        this.scroll.scrollTo(x, y, time)
      },
      finishPullUp() {
        this.scroll && this.scroll.finishPullUp()
      },
      refresh() {
        this.scroll && this.scroll.refresh()
      }
    },
  }
</script>

<style>

</style>