<template>
  <div id="cart-control">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import {vm} from '../../components/event'
  export default{
    props: {
      food: {
        type: Object
      }
    },
    created(){

    },
    methods: {
      addCart(e) {
        if (!this.food.count) {
          //console.log("1 " + JSON.stringify(this.food))
          Vue.set(this.food, 'count', 1)
          //console.log("2 " + JSON.stringify(this.food))
        } else {
          this.food.count++
        }
        vm.$emit('cartAdd', e.target)
      },
      decreaseCart(){
        if (this.food.count) {
          this.food.count--
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  #cart-control
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      transition: all 0.4s linear
      .inner
        font-size: 24px
        line-height: 24px
        color: rgb(0, 160, 220)
        display: inline-block
        transition: all 0.4s linear
        transform: rotate(0)
      &.move-enter-active, &.move-leave-active
        opacity: 1
        transform: translate3d(0, 0, 0)
      &.move-enter, &.move-leave-to
        opacity: 0
        transform: translate3d(24px, 0, 0) rotate(180deg)
    .cart-count
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 153, 159)
      display: inline-block
    .cart-add
      display: inline-block
      padding: 6px
      font-size: 24px
      line-height: 24px
      color: rgb(0, 160, 220)
</style>
