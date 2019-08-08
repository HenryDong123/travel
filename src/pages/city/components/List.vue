<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
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
          <div class="button-wrapper" v-for="item of hotCites" :key="item.id" @click="handleCityClick(item.name)">
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div
        class="area"
        v-for="(item, key) of cities"
        :key="key"
        :ref="key">
        <div class="title border-topbottom">{{key}}</div>
        <div class="item-list">
          <div class="item border-bottom" v-for="listItem of item" :key="listItem.key" @click="handleCityClick(listItem.name)">{{listItem.name}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapState, mapMutations} from 'vuex'
import Bscroll from 'better-scroll'
export default {
  name: 'CityList',
  props: {
    cities: Object,
    hotCites: Array
  },
  data () {
    return {
      letter: '',
      scrollOption: {
        click: true
      }
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper, this.scrollOption)
    this.$EventBus.$on('handleLetterChange', (e) => {
      this.letter = e
    })
  },
  computed: {
    ...mapState({currentCity: 'city'})
  },
  methods: {
    ...mapMutations(['changeCity']),
    handleCityClick (city) {
      // this.$store.dispatch('changeCity', city)
      this.changeCity(city)
      this.$router.push({name: 'Home'})
    }
  },
  watch: {
    letter () {
      if (this.letter) {
        const el = this.$refs[this.letter][0]
        this.scroll.scrollToElement(el)
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "~styles/varibles.styl"
  .border-topbottom
    &:before
      border-color: #ccc
    &:after
      border-color: #ccc
  .border-bottom
    &:before
      border-color: #ccc
  .title
    line-height .4rem
    background: #eee
    padding-left: .2rem
    color: #666
    font-size: .26rem
  .list
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    .title
      line-height: .54rem
      background: #eee
      padding-left: .2rem
      color: #666
      font-size: .26rem
    .button-list
      overflow: hidden
      padding: .1rem .6rem .1rem .1rem
      .button-wrapper
        float: left
        width: 33.33%
        .button
          margin: .1rem
          padding: .1rem 0
          text-align: center
          border: .02rem solid #ccc
          border-radius: .06rem
    .item-list
      .item
        line-height: .76rem
        padding-left: .2rem
</style>
