<template>
  <div class="recommend" ref="recommend">
    <div v-if="recommends.length" class="slider-wrapper" ref="sliderWrapper">
      <m-slider>
        <div v-for="(v, i) in recommends" :key="i">
          <a :href="v.linkUrl">
            <img :src="v.picUrl" class="needClick">
          </a>
        </div>
      </m-slider>
    </div>
    <div class="recommend-list">
      <h1>热门歌单推荐</h1>
      <ul></ul>
    </div>
    <div class="loadding-container">
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import BScroll from 'better-scroll'
import {ERR_OK} from 'api/config'
export default {
  data() {
    return {
      recommends: []
    }
  },
  created() {
    this._getRecommend()
    this._getDiscList()
  },
  methods: {
    _getRecommend() {
      this.$api.getRecommend().then((res) => {
        if (res.code === ERR_OK) {
          this.recommends = res.data.slider
        }
      })
    },
    _getDiscList() {
      this.$api.getDiscList().then((res) => {
        if (res.code === ERR_OK) {
          console.log(res.data)
        }
      })
    }
  }
}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/variable"

  .recommend
    position: fixed
    width: 100%
    top: 88px
    bottom: 0
    /*.recommend-content*/
      /*height: 100%*/
      /*overflow: hidden*/
      .slider-wrapper
        position: relative
        width: 100%
        overflow: hidden
      .recommend-list
        .list-title
          height: 65px
          line-height: 65px
          text-align: center
          font-size: $font-size-medium
          color: $color-theme
        .item
          display: flex
          box-sizing: border-box
          align-items: center
          padding: 0 20px 20px 20px
          .icon
            flex: 0 0 60px
            width: 60px
            padding-right: 20px
          .text
            display: flex
            flex-direction: column
            justify-content: center
            flex: 1
            line-height: 20px
            overflow: hidden
            font-size: $font-size-medium
            .name
              margin-bottom: 10px
              color: $color-text
            .desc
              color: $color-text-d
      .loading-container
        position: absolute
        width: 100%
        top: 50%
        transform: translateY(-50%)
</style>
