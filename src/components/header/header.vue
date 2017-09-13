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
        <div class="support">
          <span class="icon"></span>
          <span class="text"></span>
        </div>
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
    img
      display: inline-block
  .content
    display:inline-block
    margin-left:16px
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
</style>
