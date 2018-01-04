<!-- by yao -->
<template>
<div>
     <div class="shopcart">
         <!-- 底部的黑色小条 -->
         <div class="content" @click='toogleList'>
             <div class="content-left">
                   <div class="logo-wrapper">
                       <div class="logo" :class="{highlight : totalCount>0}">
                           <i class="icon-shopping_cart" :class="{highlight : totalCount>0}"></i>
                       </div>
                       <div class="num" v-if="totalCount">{{totalCount}}</div>
                   </div>
                   <div class="price">￥{{totalPrice}}</div>
                   <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
             </div>
             <div class="content-right">
                 <div class="pay" :class="totalPrice<minPrice? 'not-enough' : 'enough'">
                     {{payText}}
                 </div>
             </div>
         </div>
         <!-- 食物列表 -->
         <transition name="foodlist">
               <div class="foodlist" v-show="listShow">
                   <!-- 食物列表标题 -->
                   <div class="list-header">
                       <span class='title'>购物车</span><span class="empty" @click='clearCart'>清空</span>
                   </div>
                   <!-- 内容 -->
                   <div class="list-content" ref="listContent">
                       <ul>
                           <li class='food' v-for='food in foodList'>
                                  <span class="name">{{food.name}}/{{food.count}}个</span>
                                  <span class="price">￥{{food.price}}</span>
                                   <div class="addiconwrap">
                                    <addfoodicon :food="food" :update-food-count="updateFoodCount"></addfoodicon>
                                   </div>
                           </li>
                       </ul>
                   </div>

               </div>
         </transition>
     </div>
     <transition name="fade">
          <div class="list-mast" v-show="listShow" @click='toogleList'></div>
     </transition>
</div>
</template>

<script type='text/ecmascript-6'>
import BScroll from 'better-scroll'
import Vue from 'vue'
import addfoodicon from '../addfoodicon/addfoodicon.vue'


export default {
        props:{
            foodList: Array,
            deliveryPrice: Number,
            minPrice: Number,
            updateFoodCount: Function,
            clearCart: Function
        },
        data () {
            return {
                isShow: false
            };
        },
        computed: {
            totalCount (){
                return this.foodList.reduce((preTotal,food) => {
                    return preTotal + food.count
                },0)
            },
            totalPrice (){
                return this.foodList.reduce((preTotal,food) => {
                    return preTotal + food.count * food.price
                },0)
            },
            payText (){
                var minPrice = this.minPrice
                var totalPrice = this.totalPrice

                if(totalPrice === 0){
                    return `￥${minPrice}元起送`
                }else if(totalPrice < minPrice){
                    return `还差${minPrice - totalPrice}元起送`
                }else{
                    return '去结算'
                }
            },
            listShow (){
                if( this.totalCount === 0){
                    this.isShow = false
                    return false
                }

                if(this.isShow) {
                    Vue.nextTick(() => {
                        if(!this.scroll) {
                            this.scroll = new BScroll(this.$refs.listContent, {
                                click: true
                            })
                        }else{
                            this.scroll.refresh()
                        }
                    })
                }
                return this.isShow
            }
        },
        methods: {
               toogleList (){
                   this.isShow = !this.isShow
               }
        },
        components:{
            addfoodicon
        }

}

</script>
<style lang='stylus' rel='stylesheet/stylus'>
@import '../../common/stylus/mixins.styl';
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
                height 56px
                width 56px
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
                    &.highlight
                       color #fff
                .num
                   position absolute
                   top 0
                   right 0
                   width 24px
                   height 16px 
                   line-height 16px
                   text-align center
                   border-radius 16px
                   font-size 9px
                   font-weight 700
                   color #ffffff
                   background rgb(240,20,20)
                   box-shadow 0 4px 8px 0 rgba(0,0,0,.4)
             .price
               display inline-block
               vertical-align top
               margin-top 12px
               line-height 24px
               padding-right 12px
               box-sizing: border-box
               border-right 1px solid rgba(255,255,255,0.1)
               font-size 16px
               font-weight 700
             .desc
              display inline-block
              vertical-align top 
              margin 12px 0 0 12px
              line-height 24px
              font-size 10px
           .content-right
              flex 0 0 105px
              width 105px
              .pay 
                height 48px 
                line-height 48px 
                text-align center
                font-size 12px
                font-weight 700
                &.not-enough
                  background #2b333b
                &.enough
                  background #00b43c
                  color #fff














        .foodlist
           position absolute
           left 0
           top 0
           z-index -1
           width 100%
           transform translate3d(0,-100%,0)
           &.foodlist-enter-active,&.foodlist-leave-active
             transition all 0.5s
           &.foodlist-enter,&.foodlist-leave-active 
             transform: translate3d(0,0,0)
           .list-header
              height 40px
              line-height 40px
              border-bottom 1px solid #eeeeee
              padding 0 18px
              background #f3f5f5
              .name
                float left
                font-size 14px
                color rgb(7,17,27)
              .empty
                float right 
                font-size 12px
                color: rgb(0,160,220)

           .list-content
               padding 0 18px
               max-height 217px
               overflow hidden
               background #fff
            .food
               position relative
               padding 12px 0
               box-sizing border-box
               border-1px(rgba(7,17,27,0.1))
               .name 
                  line-height 24px 
                  font-size 14px 
                  color rgb(7,17,27)
               .price
                  position absolute
                  right 90px
                  bottom 12px
                  line-height 24px
                  font-size 14px
                  font-weight 700
                  color rgb(240,20,20)
               .addiconwrap
                  position absolute
                  right 0
                  bottom 6px
            

     .list-mast
         position fixed
         top: 0
         left 0
         width 100%
         height 100%
         z-index 40
         opacity 1
         background rgba(7,17,27,0.6)
         &.fade-enter-active,&.fade-leave-active
            transition all 0.5s
         &.fade-enter,&.fade-leave-active
            opacity 0
            background rgba(7,17,27,0)
</style>