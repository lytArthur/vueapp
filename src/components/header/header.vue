<template>
  <div class="header">
      <div class="content-wrap">
        <img width="64" height="64" :src="seller.avatar">
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
.header
  overfloe: height 
  background: rgba(7,17,27m.5)
  padding:24px 12px 18px 24px

</style>