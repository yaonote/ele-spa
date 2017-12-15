
<template>
     <div class="goods">
           <div class="menu-wrap">
                 <ul>
                       <li class="menulist" v-for="item in goods">
                             <span class='text border-1px'>
                                <span v-if="item.type >= 0" :class="classMap[item.type]"></span> {{item.name}}
                             </span>
                            
                        </li>
                 </ul>
           </div>
           <div class="food-wrap">
                <ul>
                      <li class="food-module" v-for="el in goods">
                        <div class="module-title">{{el.name}}</div>
                        <ul>
                              <li class="food-item" v-for="food in el.foods">
                                 <span>
                                    <img  :src="food.icon" alt="食物图片" width="57">
                                 </span>
                                 <div class="text-wrap">
                                    <span class="food-name">{{food.name}}</span>
                                    <span class="food-description">{{food.description}}</span>
                                    <span class="font-rating"><i>月售{{food.sellCount}}份</i><i>好评率{{food.rating}}%</i></span>
                                    <span>￥{{food.price}}</span><span v-show="food.oldPrice">￥{{food.oldPrice}}</span>
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
                   }
             })
          
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
         overflow auto        
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
               .text
                  display table-cell
                  width 56px
                  vertical-align middle
                  font-size 12px
                  border-1px(rgba(7,17,27,0.1))           
         .food-wrap
            flex 1
            overflow auto



</style>