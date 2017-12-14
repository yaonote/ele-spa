<template>
     <div class="star" :class="`star-${size}`">
          <span class="star-item" v-for="c in starClasses" :key="c.id" :class="c"></span>
     </div>
</template>

<script>
     const oneStar = 'one',
           zeroStar = 'zero',
           halfStar = 'half';
     export default {
       props: {
         score: Number,
         size: Number
       },
       computed: {
         starClasses (){
           const arrclass = []
           var score = this.score
           var scoreInteger = Math.trunc(score)
           for(let i=0; i<scoreInteger;i++){
                arrclass.push(oneStar)
           }
           if(score - scoreInteger < 5){
             arrclass.push(halfStar)
           }
           while(arrclass<5){
             arrclass.push(halfStar)
           }
           return arrclass
         }
       }
     }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .star-24
    .star-item
      display inline-block
      width 10px
      height 10px
      background-repeat no-repeat
      background-size 10px 10px
    .one
      bg-star(star24_on)
    .half
      bg-star(star24_half)
    .zero
      bg-star(star24_off)
  .star-36
    .star-item
      display inline-block
      width 15px
      height 15px
      background-repeat no-repeat
      background-size 15px 15px
    .one
      bg-star(star36_on)
    .half
      bg-star(star36_half)
    .zero
      bg-star(star36_off)
  .star-48
    .star-item
      display inline-block
      width 20px
      height 20px
      background-repeat no-repeat
      background-size 20px 20px
    .one
      bg-star(star48_on)
    .half
      bg-star(star48_half)
    .zero
      bg-star(star48_off)
</style>