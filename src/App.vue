<template>
  <div>
    <!-- 头部组件 -->
   <v-header :seller='seller'></v-header>
   <!-- 导航部分 -->
   <div class="tab border-1px">
     <div class="tab-item">
       <router-link to="/goods">商品</router-link>
     </div>
     <div class="tab-item">
       <router-link to="/ratings">评价</router-link>
      
     </div>
     <div class="tab-item">
       <router-link to="/seller">商家</router-link>
      </div>
   </div>
<!-- 中间的内容部分 -->
   <router-view>
      <div class="content">
        我是内容
      </div>
   </router-view>
  
  </div>
</template>

<script>
import  header  from "./components/header/header.vue";

const ERR_OK =0;
export default {
      data() {
          return {
             seller: {}
          }
      },
      created() {
          this.$http.get('/api/seller').then((response) => {
                response = response.body;
                if(response.errno === ERR_OK){
                    this.seller = response.data;
                    console.log(this.seller)
                }
          })
      },
      components:{
         'v-header': header
      }
}
</script>

<style lang='stylus' rel='stylesheet/stylus'>
@import './common/stylus/mixin.styl'
       .tab
          display: flex
          width: 100%
          height: 40px
          line-height: 40px
          border-1px(rgba(7,17,27,.1))
          .tab-item
            flex: 1
            text-align: center
            font: 400 14px/40px rgb(77,85,93)
            .active
              color: red
                 
</style>
