<template>
  <div>
    <div class="search">
      <input class="search-input" v-model="searchVal" type="text" placeholder="输入城市名或拼音" />
    </div>
    <div class="search-content" v-show="dataShow" ref="search">
      <ul>
        <li class="search-item border-bottom" v-for="item in list" :key="item.id">{{item.name}}</li>
        <li class="search-item border-bottom" v-show="hasNoData">
          无匹配数据
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'
export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      searchVal: '',
      list: [],
      emission: true,
      isSearch: false
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.search)
  },
  computed: {
    dataShow () {
      return !!this.searchVal
    },
    hasNoData () {
      return !this.list.length
    }
  },
  methods: {},
  watch: {
    searchVal () {
      if (this.emission) {
        setTimeout(() => {
          const result = []
          const reg = new RegExp(this.searchVal)
          for (let i in this.cities) {
            this.cities[i].forEach((item) => {
              // if (item.spell.indexOf(this.searchVal) > -1 || (item.name.indexOf(this.searchVal) > -1)) {
              //   result.push(item)
              // }
              if (reg.test(item.spell) || reg.test(item.name)) {
                result.push(item)
              }
            })
          }
          this.list = result
          console.log(this.list, '1')
          this.emission = true
        }, 100)
        this.emission = false
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .search
    height: .72rem
    padding: 0 .1rem
    background: $bgColor
    .search-input
      box-sizing: border-box
      width: 100%
      height: .62rem
      padding: 0 .1rem
      line-height: .62rem
      text-align: center
      border-radius: .06rem
      color: #666
  .search-content
    z-index: 1
    overflow: hidden
    position: absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom: 0
    background: #eee
    .search-item
      line-height: .62rem
      padding-left: .2rem
      background: #fff
      color: #666
</style>
