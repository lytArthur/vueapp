<template>
  <div class="goods" id="goods">
    <div class="menu-wrapper" ref="menuWrapper">
      <ul>
        <li v-for="(item,index) in goods " class="menu-item" :class="index" @click="selectMenu(index,$event)">
          <span class="text border-1px">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodsWrapper">
      <ul>
        <li v-for="item in goods" class="food-list" ref="foodList">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item">
              <div class="icon">
                <img :src="food.icon" height="57" width="57">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="description">{{food.description}}</p>
                <div class="extra">
                  <span>月售{{food.sellCount}}</span>
                  <span>好评率{{food.rating}}</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span v-show="food.oldPrice" class="old">￥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>

    <div class="shopcart">
      
    </div>
  </div>
</template>
<script>
import BScroll from 'better-scroll';
import shopcart from '../../components/shopcart/shopcart';
const ERR_OK = 0;
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      goods: [],
      listHeight: [],
      scrollY: 0
    }
  },
  created() {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    this.$http.get('/api/goods').then((response) => {
      response = response.body;
      if (response.errno === 0) {
        this.goods = Object.assign({}, this.goods, response.data);
        this.$nextTick(() => {
          this._initScroll()
          this._calculateHeight()
        })
      }
    });
  },
  computed: {
    currentIndex() {
      for (let i = 0; i < this.listHeight.length; i++) {
        let height1 = this.listHeight[i];
        let height2 = this.listHeight[i + 1];
        if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
          console.log(i);
          return i;
        }
      }
      return 0;
    }
  },
  methods: {
    selectMenu(index, event) {
      if (!event._constructed) {
        return
      }
      let foodList = this.$refs.foodList
      let el = foodList[index];
      console.log(el);
      this.foodsScroll.scrollToElement(el, 300);
    },
    _initScroll() {
      this.meunScroll = new BScroll(this.$refs.menuWrapper, {
        click: true
      });
      this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {
        probeType: 3
      });
      this.foodsScroll.on("scroll", (pos) => {
        this.scrollY = Math.abs(Math.round(pos.y));
      })
    },
    _calculateHeight() {
      let foodList = this.$refs.foodList
      let height = 0;
      for (let i = 0; i < foodList.length; i++) {
        let item = foodList[i];
        height += item.clientHeight;
        console.log(height);
        this.listHeight.push(height);
      }
    }
  },
  components:{
    shopcart
  }
}
</script>

<style lang="stylus" scoped>
  @import  '../../common/stylus/minix'
.goods
  width: 100%
  display: flex
  overflow: hidden
  position: absolute
  top: 174px
  bottom: 46px
  .menu-wrapper
    flex: 0 0 80px
    width: 80px
    background: #f3f5f7
    .menu-item
      display: table
      height: 54px
      width: 56px
      padding: 0 12px
      line-height: 14px
      &.current
        position: relative
        z-index: 10
        margin-top: -1px
        background: #fff
        font-weight: 700
        .text
          border-none()
      .text
        display: table-cell
        width: 56px
        vertical-align: middle
        font-size: 12px
        border-1px("rgba(7,17,27,0.1)")
        .icon
          display: inline-block
          vertical-align: top
          width: 12px
          height: 12px
          margin-right: 2px
          background-size: 12px 12px
          background-repeat: no-repeat
          &.decrease
            bg-image('decrease_3')
          &.discount
            bg-image('discount_3')
          &.guarantee
            bg-image('guarantee_3')
          &.invoice
            bg-image('invoice_3')
          &.special
            bg-image('special_3')
  .foods-wrapper
    flex: 1
    background: #ffffff
    .title
      padding-left: 14px
      height: 26px
      line-height: 26px
      border-left: 2px solid #d9dded
      font-size: 12px
      color: rbga(147,153,159)
      background: #f3f5f7
    .food-item
      display: flex
      margin: 18px
      border-1px(rgba(7,17,27,0.2))
      &:last-child
        margin-bottom: 0
        border-none()
      .icon
        flex: 0 0 57px
        margin-right: 10px
      .content
        flex: 1
        .name
          margin: 2px 0 8px 0
          font-size: 14px
          line-height: 14px
          color: rgb(7,17,27)
        .description
          line-height: 10px
          font-size: 10px
          color: rgb(147,153,159)
          margin-bottom: 8px
        .extra
          line-height: 10px
          font-size: 10px
          color: rgb(147,153,159)
        .price
          font-weight: 700
          line-height: 24px
          .now
            margin-right: 8px
            font-size: 14px
            color: rgb(240,20,20)
          .old
            color: rgb(147,153,159) 
</style>