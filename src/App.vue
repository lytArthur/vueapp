<template>
  <div class="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">商品</div>
      <div class="tab-item">评论</div>
      <div class="tab-item">商家</div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import header from './components/header/header.vue';
const middleOK = 0;
export default {
  data() {
    return {
      seller:  {}
    }
  },
  created() {
    this.$http.get('/api/seller').then((response) => {
      response = response.body;
      if (response.errno === 0) {
        this.seller = Object.assign({}, this.seller, response.data);
      }
      console.log(response);
    });
  },
  components: {
    'v-header': header
  }
}
</script>

<style lang="stylus" scoped>
.tab
  display: flex
  width: 100%
  height: 40px
  line-height:40px
  .tab-item
     flex: 1
     text-align: center
</style>

