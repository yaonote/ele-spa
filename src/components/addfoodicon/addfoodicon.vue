<template>
 <div class="addfoodicon">
     <transition name="reduce">
          <span class="reduce icon-remove_circle_outline" v-show="food.count"
          @click.stop='updateFoodCount(food,false,$event)'>
          </span>
     </transition>
         
          <span class="sum" v-show='food.count'>{{food.count}}</span>
          <span class="add icon-add_circle" @click.stop='updateFoodCount(food,true,$event)'></span>
 </div>
</template>

<script type="text/ecmascript-6">
 export default {
     props: {
         food: Object,
         updateFoodCount: Function
     }
   
 }
</script>

<style scoped lang="stylus">
     .addfoodicon
         font-size 0
         .add
             display inline-block
             padding 6px
             line-height 24px
             font-size 24px
             color: rgb(0,160,220)
         .sum
             display inline-block
             vertical-align top
             width 12px
             padding-top 6px
             line-height 24px 
             text-align center
             font-size 10px
             color rgb(147,153,159)
         .reduce
             display inline-block
             padding 6px
             line-height 24px
             font-size 24px
             color rgb(0,160,220)
             &.reduce-enter-active, &.reduce-leave-active
               transition: all .4s linear
             &.reduce-enter, &.reduce-leave-active
               opacity: 0
               transform: translate3d(24px, 0, 0) rotate(180deg)
 
</style>
