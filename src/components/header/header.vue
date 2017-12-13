<!-- by yao -->
<template>
     <div class="header-wrap">
       <!-- 主要内容 -->
         <div class="content-wrap">
           <!-- 头像 -->
               <div class="avatar">
                    <img :src="seller.avatar" alt="头像" width="64" height="64">
               </div>
               <!-- 文本 -->
               <div class="content">
                     <div class="title">
                       <span class="brand"></span>
                       <span class="name">{{seller.name}}</span>
                     </div>
                     <div class="description">
                       {{seller.description}}/{{seller.deliveryTime}}分钟
                     </div>
                     <div v-if="seller.supports" class="supports">
                       <span class="icon" :class="classMap[seller.supports[0].type]"></span>
                       <span class="text">{{seller.supports[0].description}}</span>
                     </div>
                     <!-- 右侧的数量显示 -->
                     <div class="supports_count" v-if="seller.supports" @click="showDetail(true)">
                     <span>{{seller.supports.length}}个></span>
                     </div>
                   
               </div>
         </div>
         <!-- 公告部分 -->
         <div class="bulletin">
           <span class="bulletin-icon"></span>
           <span class="bulletin-text">{{seller.bulletin}}</span>
           <span class="more">></span>
         </div>
         <!-- 模糊背景 -->
         <div class="bgc">
             <img :src="seller.avatar" alt="模糊背景">
         </div>
           <!-- 弹出层 -->
           <transition name="grey">
                     <div class="grey" v-show="detailShow">
                         <div class="big_name">{{seller.name}}</div>
                         <div class="star"></div>
                         <div class="module-title">
                           <span class="line"></span>
                           <span class="module-text">优惠信息</span>
                           <span class="line"></span>
                         </div>
                         <!-- 优惠信息内容 -->
                         <ul class="supports" v-if="seller.supports">
                              <li class="support" v-for="item in seller.supports" v-bind:key="item">
                                <span>{{item.description}}</span>
                              </li>
                         </ul>
                         <!-- 商家公告 -->
                         <div class="module-title">
                           <span class="line"></span>
                           <span class="module-text">商家公告</span>
                           <span class="line"></span>
                         </div>
                         <div class="grey-bulletin">
                           {{seller.bulletin}}
                         </div>
                     </div>
         </transition>

     </div>
    
    
</template>

<script type='text/ecmascript-6'>
export default {
  props: {
     seller: {
         type: Object
     }
  },
  data (){
    return {
        detailShow: false
    }
  },
  methods:{
     showDetail (isShow){
       this.detailShow = isShow
     }
  },
  created(){
    this.classMap = ['decrease','discount','guarantee','invoice','special']
  }
};

</script>
<style lang='stylus' rel='stylesheet/stylus'>
    @import "../../common/stylus/mixin";
     .header-wrap
       position relative
       color: #ffffff
       background rgba(7,17,27,.5)
       .content-wrap
         padding: 24px 12px 18px 24px
         font-size: 0
         .avatar
           display inline-block
           vertical-align top
           img 
            border-radius 2px
         .content
           position relative
           display inline-block
           margin-left 16px
           font-size: 14px
           .title
             margin 2px 0 8px 0
             .brand
                width 30px
                height 18px
                display inline-block
                vertical-align top
                bg-image('brand')
                background-size: 30px 18px
                background-repeat no-repeat
             .name
                margin-left 6px
                font-size 16px
                line-height 18px
                font-weight bold
           .description
             margin: 8px auto 10px
             font-size: 12px
           .supports
             font-size 10px
             .icon
                display inline-block
                width 12px
                height 12px
                margin-right 4px
                margin-top 1px
                vertical-align top
                background-size 12px 12px
                background-repeat no-repeat
                &.decrease
                  bg-image('decrease_1')
                &.discount
                  bg-image('discount_1')
                $.guarantee
                  bg-image('guarantee_1')
                $.invoice
                  bg-image('invoice_1')
                $.special
                  bg-image('special_1')
           .supports_count
              position absolute
              bottom -10px
              right  -70px
              width  60px 
              height 30px
              line-height 30px
              font-size 10px
              text-align center
              border-radius 15px
              background rgb(0,0,0,.2)
       .bulletin
          position relative
          height 28px 
          line-height 28px
          padding  0 12px
          overflow hidden
          white-space nowrap
          text-overflow: ellipsis
          background rgba(7,17,27,0.2)
          .bulletin-icon
             display inline-block
             width 22px
             height 12px
             bg-image(bulletin)
             background-size 22px 12px
             background-repeat no-repeat
             vertical-align middle
          .bulletin-text
              height 28px
              line-height 28px
              font-size 10px
              margin 0 4px
          .more
              position absolute
              top 0px
              right 5px
       .bgc
         position absolute
         top 0
         right 0
         bottom 0
         left 0
         z-index -1
         filter blur(10px)
         img 
           width 100%
           height 100%
       .grey
         position fixed
         top 0
         left 0
         z-index 100
         background  rgba(7,17,27,.8)
         text-align center
         .big_name
            margin-top 64px
            font 700 16px/32px ""
         .star
           height 24px
           margin 16px auto 28px
           border 1px solid red
         .module-title
           padding 36px 0
           .line
              display inline-block
              width 112px
              border-top 1px solid rgba(255,255,255,.2)
         .grey-bulletin
            margin-top 24px
            padding 0 48px
            font 12px/24px ""
            text-align justify



       
      



   
   





</style>