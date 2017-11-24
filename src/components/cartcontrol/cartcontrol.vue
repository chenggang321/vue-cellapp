<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import bus from 'components/eventbus/eventbus.js';
  import Vue from 'vue';
  export default {
    props: {
      food: {
        type: Object
      }
    },
    name: 'cartcontrol',
    methods: {
      addCart (event) {
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
        bus.$emit('cart.add', event.target);
      },
      decreaseCart () {
        if (this.food.count) {
          this.food.count--;
        }
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet">
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      &.move-enter-active, &.move-leave-active
        transition: all 0.4s linear
        .inner
          transition: all 0.4s linear
      &.move-enter-to, &.move-leave
        opacity: 1
        transform: translate3D(0, 0, 0)
        .inner
          transform: rotate(0)
      &.move-enter, &.move-leave-to
        opacity: 0
        transform: translate3D(24px, 0, 0)
        .inner
          transform: rotate(180deg)
      .inner
        display: inline-block
        padding: 6px
        font-size: 24px
        line-height: 24px
        color: rgb(0, 160, 220)
    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      font-size: 10px
      color: rgb(147, 153, 159)
      text-align: center
    .cart-add
      display: inline-block
      padding: 6px
      font-size: 24px
      line-height: 24px
      color: rgb(0, 160, 220)
</style>
