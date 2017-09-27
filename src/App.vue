<template>
  <div class="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>

    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <!-- keep-alive是vue 内置的一个组件可以使包含的组件能够保留状态，避免被重新渲染 -->
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>

  </div>
</template>

<script type="text/ecmascript-6">
import header from './components/header/header.vue';
const middleOK = 0;
export default {
  data() {
    return {
      seller: {}
    }
  },
  created() {
    this.$http.get('/api/seller').then((response) => {
      response = response.body;
      if (response.errno === 0) {
        this.seller = Object.assign({}, this.seller, response.data);
      }
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

