<!-- by yao -->
<template>
     <div class="shopcart">
         <div class="content">
             <div class="content-left">
                   <div class="logo-wrapper">
                       <div class="logo">
                           <i class="icon-shopping_cart"></i>
                       </div>
                       <div class="num" v-if="totalCount"></div>
                   </div>
                   <div class="price"></div>
                   <div class="desc">另需配送费￥元</div>
             </div>
             <div class="content-right">
                 <div class="pay">
                     还差￥10起送
                 </div>
             </div>
         </div>
     </div>
</template>

<script type='text/ecmascript-6'>
export default {
  data () {
    return {
        totalCount: false
    };
  }

}

</script>
<style lang='stylus' rel='stylesheet/stylus'>
     .shopcart
        position: fixed
        bottom: 0
        left: 0
        z-index: 50
        width: 100%
        height: 48px
        .content
           display: flex
           background: #141d27
           font-size: 0
           color: rgba(255,255,255,0.4)
           .content-left
             flex: 1
             .logo-wrapper
                display inline-block
                vertical-align top
                position relative
                top -10px
                margin 0 12px
                padding 6px
                box-sizing border-box
                border-radius 50%
                background #141d27
                .logo
                  width 100%
                  height 100%
                  border-radius 50%
                  text-align center
                  background #2b343c
                  &.highlight
                    background rgb(0,160,220)
                  .icon-shopping_cart
                    line-height 44px
                    font-size 24px
                    color #80858a
                    &.heightlight
                      color #fff

</style>