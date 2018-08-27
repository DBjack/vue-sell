<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar"> <!--左侧商家头像-->
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title"> <!--标题-->
          <span class="brand"></span>
          <span class="name">{{ seller.name }}</span>
        </div>
        <div class="description"> <!--描述-->
          {{ seller.description }}/{{ seller.deliveryTime }}分钟送达
        </div>
        <div v-if="seller.supports" class="support"> <!--支持的活动-->
          <span class="icon" :class="classMap[seller.supports[0].type]"></span><!--满减 折扣 套餐 发票 保障等图标-->
          <span class="text">{{ seller.supports[0].description }}</span> <!--默认取第0个活动-->
        </div>
      </div>
      <div v-if="seller.supports" class="support-count"> <!--活动个数-->
        <span class="count">{{ seller.supports.length }}个</span>
        <span class="icon-keyboard_arrow_right"></span> <!--右箭头-->
      </div>
    </div>
    <div class="bulletin-wrapper"> <!--公告-->
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{ seller.bulletin }}</span>
      <span class="icon-keyboard_arrow_right"></span> <!--右箭头-->
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      seller: {
        type: Object
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/mixin.styl'; // 此处不可用alias省略
  
  .header
    background: #728080
    color: #fff
    .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avatar
        display: inline-block
        vertical-align: top
        img
          border-radius: 2px
      .content
        display: inline-block
        margin-left 16px
        font-size: 14px
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-size: 16px
            line-height: 18px
            font-weight: bold
        .description
          margin-bottom: 10px
          line-height: 12px
          font-size: 12px;
        .support
          font-size: 0
          .icon
            display: inline-block
            vertical-align: top
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
          .text
            line-height: 12px
            font-size: 10px
      .support-count
        position: absolute
        right: 12px
        bottom: 14px
        padding: 0 8px
        height: 24px
        line-height: 24px
        border-radius: 14px
        background-color: rgba(0,0,0,0.2)
        text-align: center
        .count
          vertical-align: top
          font-size: 10px
        .icon-keyboard_arrow_right
          margin-left: 2px
          line-height: 24px
          font-size: 10px
</style>
