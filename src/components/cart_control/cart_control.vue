<template>
  <div class="cart_control">
    <div class="cart_decrease " v-show="food.count>0"
       @click="decreaseCart" transition="move">
       <span class="inner icon-remove_circle_outline"></span>
       </div>
    <div class="cart_count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart_add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script>
import Vue from 'vue';
export default {
  props: {
    food: {
      type: Object
    }
  },
  created () {

  },
  methods: {
    addCart (event) {
      if (!event._constructed) {
        return;
      };
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1);
      } else {
        this.food.count++;
      }
      this.$dispatch('cart.add', event.target);
    },
    decreaseCart (event) {
      if (!event._constructed) {
        return;
      };
      if (this.food.count) {
        this.food.count--;
      };
    }
  }
};
</script>

<style lang="stylus">
  .cart_control{
    font-size 0
    .cart_decrease{
      display inline-block
      padding 6px
      transition all 0.4s linear
      &.move-transition{
        opacity 1
        transform translate3d(0, 0, 0)
        .inner{
          display inline-block
          font-size 24px
          line-height 24px
          color rgb(0, 160, 220) 
          transition all 0.4s linear
          transform rotate(0)
        }  
      }
      
      &.move-enter, &.move-leave{
        opacity 0
        transform translate3d(24px, 0, 0)
        .inner{
          transform rotate(180deg)    
        }
      }
        
    } 
    .cart_count{
      display inline-block
      font-size 10px
      vertical-align top
      width 24px
      line-height 24px
      text-align center
      padding-top 6px
      color rgb(147, 153, 159)
    } 
    .cart_add{
      display inline-block
      font-size 24px
      line-height 24px
      padding 6px
      color rgb(0, 160, 220)
    }
}
</style>
