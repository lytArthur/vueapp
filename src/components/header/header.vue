<template>
  <div class="header">
    <div class="content-warper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟到达
        </div>
        <!-- if 判断数据请求过来之后再渲染 -->
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="detialShowAbove">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>

    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>

    <div class="showDetail" v-show="detialShow" @click="detialShowAbove">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <div class="star-wraper">

          </div>
        </div>
        <!-- <div class="discount-line">
          <div class="line"></div>
          <div class="center-text">优惠信息</div>
          <div class="line"></div>
        </div> -->
      </div>

      <div class="detail-close">
         <i class="icon-close"></i>
      </div>
    </div>

  </div>
</template>
<script type="text/ecmascript-6">
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      detialShow: false
    }
  },
  methods: {
    detialShowAbove() {
      this.detialShow = true
    }
  },
  created() {
    console.log(this);
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
  }
}
</script>
<style lang="stylus" scoped>
 @import "../../common/stylus/minix"

.header
  overflow: hidden 
  background: rgba(7,17,27,0.5)
  position: relative
  .content-warper
    position: relative
    padding: 24px 12px 18px 24px
    font-size: 0
    .avatar
      display: inline-block
      vertical-align: top
    img
      display: inline-block
  .content
    display:inline-block
    margin-left:16px
    vertical-align: top
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
        display:inline-block
        line-height: 18px
        font-weight: bold
        margin-left: 6px
        font-size: 16px
    .description
      line-height: 12px
      font-size: 12px
      margin-bottom: 10px
  .support
    .icon
      display: inline-block
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
      display: inline-block
      vertical-align: top
  .bulletin-wrapper
    position: relative
    height: 28px
    line-height: 28px
    padding: 0 22px 0 12px
    white-space: nowrap
    overflow: hidden
    text-overflow: ellipsis
    background: rgba(7, 17, 27, 0.2)
    .bulletin-title
      display: inline-block
      vertical-align: top
      margin-top: 8px
      width: 22px
      height: 12px
      bg-image('bulletin')
      background-size: 22px 12px
      background-repeat: no-repeat
    .bulletin-text
      vertical-align: top
      margin: 0 4px
      font-size: 10px
    .icon-keyboard_arrow_right
      position: absolute
      font-size: 10px
      right: 12px
      top: 10px
  .support-count
    position: absolute
    right: 12px
    bottom: 14px
    padding: 0 8px
    height: 24px
    line-height: 24px
    border-radius: 14px
    background: rgba(0, 0, 0, 0.2)
    text-align: center
    .count
      vertical-align: top
      font-size: 10px
     .icon-keyboard_arrow_right
        margin-left: 2px
        line-height: 24px
        font-size: 10px
  .showDetail
    width: 100%
    height: 100%
    background: rgba(7,17,27,0.8)
    backdrop-filter: blur(10px)
    position:fixed
    top: 0
    left: 0
    z-index: 9
    .detail-wrapper
      width: 100%
      min-height: 100%
      .detail-main
        // margin-top: 60px
        padding-top: 64px
        .name
          color: #ffffff
          font-size: 16px
          font-weight: 700
          text-align: center
          line-height: 16px
    .detail-close
      width: 32px
      height: 32px
      position: relative;
      margin: -64px auto 0 auto
      font-size: 32px
      clear both
      colo: #fff
</style>
