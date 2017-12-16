<template>
<div class="goods">
      <!-- 左侧的菜单 -->
      <div class="menu-wrap" ref="menuwrap">
      <ul>
            <li class="menulist" v-for="(item,index) in goods"
                 :class="{current: index === 0}">
                  <span class='text border-1px'>
                        <span v-if="item.type >= 0" :class="classMap[item.type]" class="icon"></span>
                         {{item.name}}
                  </span>
                  
            </li>
      </ul>
      </div>
      <!-- 右测的食物区 -->
      <div class="food-wrap" ref="foodwrap">
      <ul>
            <li class="food-module" v-for="el in goods">
                  <div class="module-title">{{el.name}}</div>
                  <ul>
                  <li class="food-item" v-for="food in el.foods">
                        <span class="img-wrap">
                           <img  :src="food.icon" alt="食物图片" width="57">
                        </span>
                        <div class="text-wrap">
                              <span class="food-name">{{food.name}}</span>
                              <span class="food-description">{{food.description}}</span>
                              <span class="food-rating">
                                    <span class="text">月售{{food.sellCount}}份</span><span class="text">好评率{{food.rating}}%</span>
                              </span>
                              <span class="price">￥{{food.price}}
                                 <span v-show="food.oldPrice" class="oldprice">￥{{food.oldPrice}}</span>
                              </span>
                              <span class="addiconwrap">
                                    <addfoodicon :food="food" :update-food-count="updateFoodCount"></addfoodicon>
                              </span>
                        </div>
                  </li>
                  </ul>            
            </li>
      </ul>
      </div>
</div>
</template>

<script type='text/ecmascript-6'>
import axios from 'axios'
import BScroll from 'better-scroll'
import Vue from 'vue'

import addfoodicon from '../addfoodicon/addfoodicon.vue'
const ERR_OK = 0;
export default {
       
       props: ['seller'],
       data(){
             return {
                 goods: []
             }
       },
       created() {
             this.classMap = ['decrease','discount','special','invoice','gurantee']
             axios.get('/api/goods').then(response => {
                   const result = response.data
                   if(result.errno === 0){
                        this.goods = result.data
                        console.log(result.data)
                        Vue.nextTick(() => {
                              this._initScroll()
                        })
                       
                   }
             })
          
       },
       methods: {
             _initScroll (){
                   new BScroll(this.$refs.menuwrap,{
                         click: true
                   })
                   this.foodsScroll = new BScroll(this.$refs.foodwrap,{
                         probeType: 3,
                         click: true
                   })
             },
             updateFoodCount (food,isAdd,event){
                     if(!event._constructed){
                           return
                     }
                     if(isAdd){
                           if(!food.count){
                              console.log('没有菜')
                              Vue.set(food,'count',1)
                           }else {
                              food.count++
                           }                         
                     }else{
                           if(food.count){
                                 food.count--
                           }
                     }
             }
       },
       components: {
             addfoodicon
       }
}

</script>
<style lang='stylus' rel='stylesheet/stylus'>
@import '../../common/stylus/mixin.styl'

      .goods
         display flex
         position absolute
         top 174px
         bottom 46px
         width 100%
         overflow hidden        
         .menu-wrap
            flex 0 0 80px
            width 80px  
            background #f3f5f7         
            .menulist
               display table
               height 54px
               width 56px
               padding 0 12px
               line-height 14px
               &.current
                  background #fff
               .text
                  display table-cell
                  width 56px
                  vertical-align middle
                  font-size 12px
                  border-1px(rgba(7,17,27,0.1)) 
                  .icon
                    display inline-block
                    vertical-align top
                    width 12px 
                    height 12px
                    margin-right 2px
                    background-size 12px 12px 
                    background-repeat no-repeat
                    &.decrease
                      bg-image('decrease_3')  
                    &.discount
                      bg-image('discount_3')
                    &.guarantee
                      bg-image('guarantee_3')
                    &.invoice
                      bg-iamge('invoice_3')
                    &.special
                      bg-image('special_3')        
         .food-wrap
             flex 1
            .food-module
               flex 1             
               .module-title
                  height 26px
                  border-left 2px solid #d9dded 
                  background #f3f5f7
                  line-height 26px
                  padding-left 12px
                  font-size 12px
                  color rgb(147,153,159)
               .food-item
                  position relative
                  flex 1
                  margin 18px
                  padding-bottom 18px
                  border-bottom  1px solid rgba(7,17,27,.1)
                  .img-wrap
                     display inline-block
                     margin-right 10px  
                     vertical-align top                   
                  .text-wrap
                     display inline-block
                     span 
                        display block
                     .food-name
                        font-size 14px
                        color rgb(7,17,27)
                        line-height 14px
                     .food-description
                        margin 8px 0
                        font-size 10px
                        line-height 14px
                        width 120px
                     .food-rating
                        .text 
                           display inline-block                        
                           font-size 10px
                           line-height 10px
                           margin-right 12px
                     .price 
                        margin-top 8px
                        font 700 14px/24px
                        color rgb(240,20,20) 
                        .oldprice
                           display inline-block
                           font-size 10px
                           color rgb(147,153,159)
                     .addiconwrap
                        position absolute
                        right 0
                        bottom 8px
            
 

</style>