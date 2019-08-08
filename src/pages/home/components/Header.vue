<template>
  <div class="header">
    <div class="header-left">
      <div class="back-icon"><i class="iconfont iconfanhui"></i></div>
    </div>
    <div class="header-input">
      <i class="iconfont iconsousuo"></i>
      输入城市/景点/游玩主题
    </div>
    <router-link :to="{name: 'City'}">
      <div class="header-right">
        <p>
          {{this.city}}
        </p>
        <span class=" arrow-icon"><i class="iconfont iconjiantou"></i></span>
      </div>
    </router-link>

  </div>
</template>

<script>
import {mapState} from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .header
    display: flex
    line-height: .86rem
    background: $bgColor
    color: #fff
    .header-left
      flex-basis: .64rem
      flex-shrink: 0
      .back-icon
        text-align: center
        font-size: .4rem
    .header-input
      flex: 1
      height: .64rem
      line-height: .64rem
      margin-top: .12rem
      margin-left: .2rem
      padding-left: .2rem
      background: #fff
      border-radius: .1rem
      color: #ccc
    .header-right
      flex-basis: 1.3rem
      flex-shrink: 0
      display: flex
      margin: 0 .2rem
      text-align: center
      color: #fff
      p
        white-space nowrap
        text-overflow: ellipsis
        overflow: hidden
      .arrow-icon
        margin-left: -.04rem
        font-size: .24rem
</style>
