<template>
  <div>
    <router-link
      tag='div'
      to='/'
      class="header-abs"
      v-show="showAbs"
    >
      <div class="iconfont header-back">&#xe624;</div>
    </router-link>
    <div
      class="header-fixed"
      v-show="!showAbs"
      :style="opacityStyle"
    >
      <router-link to="/">
        <div class="iconfont header-fixed-back">&#xe624;</div>
      </router-link>
      景点详情
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) { // 过渡阶段
        let opacity = top / 140 // 过渡效果
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = { opacity }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  },
  activated () {
   window.addEventListener('scroll', this.handleScroll) // 页面展示绑定
  },
  deactivated  () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl';
  .header-abs
    position absolute
    left .2rem
    top .2rem
    width .6rem
    height .6rem
    text-align center
    line-height .6rem
    border-radius .3rem
    background rgba(0,0,0,.6)
    .header-back
      color #fff
      font-size .3rem
  .header-fixed
    z-index 2
    position fixed
    top 0
    left 0
    right 0
    height $headerHeight
    line-height $headerHeight
    text-align center
    color #fff
    background-color $bgcolor
    font-size .32rem
    .header-fixed-back
      position absolute
      top 0
      left .1rem
      text-align center
      font-size .4rem
      color #fff
</style>
