<template>
  <div class="recommend" ref="recommend">
    <div v-if="recommends.length"  class="slider-wrapper">
      <slider>
        <div v-for="(item,index) in recommends" :key="index">
            <a :href="item.linkUrl">
                <img :src="item.picUrl" />
            </a>
        </div>
      </slider>
    </div>
 
  </div>
</template>

<script type="text/ecmascript-6">
import { getRecommend} from '../../api/recommend'
import { ERR_OK } from '../../api/config'
import Slider from '../../bases/silder/silder'
export default {
    data(){
      return{
        recommends: []
      }
    },
    created(){
        this._getRecommend();
       
    },
    methods: {
        _getRecommend(){
            getRecommend().then((res)=>{
                if(res.code === ERR_OK){
                    this.recommends = res.data.slider
                    //console.log(res.data.slider);
                }
            })
        },
        _getDiscList(){
          getDiscList().then((res)=>{
            if(res.code === ERR_OK){
              console.log(res.data.list);
            }
          })
        }
    },
    components: {
      Slider
    }
}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/variable"
  .recommend
    position: fixed
    width: 100%
    top: 88px
    bottom: 0
    .recommend-content
      height: 100%
      overflow: hidden
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