<template>
  <div id="app">
    <v-header v-if="seller" :seller = "seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to='/goods'>商品信息</router-link>
      </div>
      <div class="tab-item">
        <router-link to='/ratings'>评价栏信息</router-link>
      </div>
      <div class="tab-item">
        <router-link to='/sellers'>商家信息</router-link>
      </div>
    </div>
    <div class="content">
       <router-view :seller = "seller"></router-view>
    </div>
    <hide :seller = "seller"></hide>
  </div>
</template>

<script>
import header from './components/header'
import goods from './components/goods'
import hide from './components/hide'
import axios from 'axios'

export default {
  name: 'App',
  data () {
    return {
      seller : {},
      items : true,
      rating : false,
      business : false
    }
  },
  components : {
    'v-header' : header,
    goods,
    hide
  },
  created () {
    axios.get('/good/seller').then(
      res => {
        if(res.data.code === 0){
          this.seller = res.data.data
        }
      }
    )
  }
}
</script>

<style lang='stylus' ref='stylesheet/stylus'>
  @import 'assets/stylus/index.styl';
  #app
    .tab
     display flex
     height 40px
     line-height 40px
     border-1px(rgba(240,20,20,0.1))
     .tab-item
          flex 1
          text-align center
          font-size 14px
          color rgb(77,85,93)
          a
            width 100%
            height 100%
            display block
            &:visited
              color #000
          .router-link-active
            color rgb(240,20,20) !important
</style>
