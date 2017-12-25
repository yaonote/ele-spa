<template>
 <div class="addfoodicon">
          <span class="reduce icon-remove_circle_outline" v-show="food.count"
          @click.stop='updateFoodCount(food,false,$event)'>
          </span>
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
             display inline-block!important
             padding 6px
             line-height 24px
             font-size 24px
             color: rgb(0,160,220)
         .sum
             display inline-block!important
             vertical-align top
             width 12px
             padding-top 6px
             line-height 24px 
             text-align center
             font-size 10px
             color rgb(147,153,159)
         .reduce
             display inline-block!important
             padding 6px
             line-height 24px
             font-size 24px
             color rgb(0,160,220)
 
</style>
