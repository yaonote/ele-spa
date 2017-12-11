<!-- by yao -->
<template>
     <div class="header-wrap">
         <div class="content-wrap">
               <div class="avatar">
                    <img :src="seller.avatar" alt="头像" width="64" height="64">
               </div>
               <div class="content">
                     <div class="title">
                       <span class="brand"></span>
                       <span class="name">{{seller.name}}</span>
                     </div>
                     <div class="description">
                       {{seller.description}}/{{seller.deliveryTime}}分钟
                     </div>
                     <div v-if="seller.supports" class="supports">
                       <span class="icon"></span>
                       <span class="text">{{seller.supports[0].description}}</span>
                     </div>
               </div>
         </div>
         <div class="head-main">

         </div>

     </div>
    
    
</template>

<script type='text/ecmascript-6'>
export default {
  props: {
     seller: {
         type: Object
     }
  }
};

</script>
<style lang='stylus' rel='stylesheet/stylus'>
     .header-wrap
       color: #ffffff
       background-color #999999
       .content-wrap
         padding: 24px 12px 18px 24px
         font-size: 0
         .avatar
           display inline-block
         .content
           display inline-block
           margin-left 16px
           font-size: 14px
           .title
             margin 2px 0 8px 0
             .brand
                width 30px
                height 18px
                display inline-block

</style>