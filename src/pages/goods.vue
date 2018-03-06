<template>
  <div class="goods">
    <div class="goods-container">
      <div class="menu-wrapper">
        <ul>
          <li v-for="(item,index) in goods" :key="index" class="menu-item" :class="{'current':currentIndex===index}"
              @click="selectMenu(index,$event)" ref="menuList">
          <span class="text">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
          </span>
          </li>
        </ul>
      </div>
      <div class="foods-wrapper">
        <ul>
          <li v-for="(item, index) in goods" :key="index" class="food-list" ref="foodList">
            <h1 class="title">{{item.name}}</h1>
            <ul>
              <li @click="selectFood(food,$event)" v-for="(food, index) in item.foods" :key="index" class="food-item border-1px">
                <div class="icon">
                  <img width="114" height="114" :src="food.icon">
                </div>
                <div class="content">
                  <h2 class="name">{{food.name}}</h2>
                  <p class="desc">{{food.description}}</p>
                  <div class="extra">
                    <span class="count">月售{{food.sellCount}}份</span><span>好评率{{food.rating}}%</span>
                  </div>
                  <div class="price">
                    <span class="now">￥{{food.price}}</span><span class="old"
                                                                  v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                  </div>
                  <div class="cartcontrol-wrapper">
                    <!-- <cartcontrol @add="addFood" :food="food"></cartcontrol> -->
                  </div>
                </div>
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
const ERR_OK = 0
const debug = process.env.NODE_ENV !== 'production'

export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      goods: []
    }
  },
  created() {
    console.log(111)
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    this.getData()
  },
  computed: {
    currentIndex() {
      return 0
    }
  },
  methods: {
    getData() {
      const url = debug ? '/api/goods' : 'http://ustbhuangyi.com/sell/api/goods'
      this.$http
        .get(url)
        .then(res => {
          let resp = res.data
          if (resp.errno === ERR_OK) {
            this.goods = resp.data
            // this.$nextTick(() => {
            //   this.scroll = new BScroll(this.$refs.ratings, {
            //     click: true
            //   })
            // })
          }
        })
        .catch(err => {
          console.log(err)
        })
    },
    selectMenu() {},
    selectFood() {}
  }
}
</script>
<style lang="less">
@import '../common/style/mixin.less';

@bs: 46.875rem;
.bg-image(@path) {
  background-image: url('@{path}@2x.png');
}
.goods-container {
  display: flex;
  position: absolute;
  top: 352/@bs;
  bottom: 0;
  left: 0;
  overflow: hidden;
  width: 100%;
  background-color: #f3f5f7;
  .menu-wrapper {
    flex: 0 0 160/@bs;
    width: 160/@bs;
    background: #f3f5f7;

    .menu-item {
      display: table;
      height: 108/@bs;
      width: 112/@bs;
      padding: 0 24/@bs;
      line-height: 28/@bs;

      &.current {
        position: relative;
        z-index: 10;
        margin-top: -1px;
        background: #fff;
        font-weight: 700;

        .text {
          border: none;
        }
      }

      .icon {
        display: inline-block;
        vertical-align: top;
        width: 24/@bs;
        height: 24/@bs;
        margin-right: 4/@bs;
        background-size: 24/@bs 24/@bs;
        background-repeat: no-repeat;

        &.decrease {
          .bg-image('../assets/decrease_2');
        }

        &.discount {
          .bg-image('../assets/discount_2');
        }

        &.guarantee {
          .bg-image('../assets/guarantee_2');
        }

        &.invoice {
          .bg-image('../assets/invoice_2');
        }

        &.special {
          .bg-image('../assets/special_2');
        }
      }

      .text {
        display: table-cell;
        width: 112/@bs;
        vertical-align: middle;
        .border-1px(rgba(7, 17, 27, 0.1));
        font-size: 24/@bs;
      }
    }
  }
  .foods-wrapper {
    flex: 1;
    background-color: #fff;
    .title {
      padding-left: 28/@bs;
      height: 52/@bs;
      line-height: 52/@bs;
      border-left: 2px solid #d9dde1;
      font-size: 24/@bs;
      color: rgb(147, 153, 159);
      background: #f3f5f7;
    }

    .food-item {
      display: flex;
      margin: 36/@bs;
      padding-bottom: 36/@bs;
      .border-1px(rgba(7, 17, 27, 0.1));

      &:last-child {
        border: none;
        margin-bottom: 0;
      }

      .icon {
        flex: 0 0 114/@bs;
        margin-right: 20/@bs;
      }

      .content {
        flex: 1;

        .name {
          margin: 4/@bs 0 16/@bs 0;
          height: 28/@bs;
          line-height: 1;
          font-size: 28/@bs;
          color: rgb(7, 17, 27);
        }

        .desc,
        .extra {
          line-height: 1;
          font-size: 20/@bs;
          color: rgb(147, 153, 159);
        }

        .desc {
          line-height: 24/@bs;
          margin-bottom: 16/@bs;
        }

        .extra {
          .count {
            margin-right: 24/@bs;
          }
        }

        .price {
          font-weight: 700;
          line-height: 48/@bs;

          .now {
            margin-right: 16/@bs;
            font-size: 28/@bs;
            color: rgb(240, 20, 20);
          }

          .old {
            text-decoration: line-through;
            font-size: 20/@bs;
            color: rgb(147, 153, 159);
          }
        }

        .cartcontrol-wrapper {
          position: absolute;
          right: 0;
          bottom: 24/@bs;
        }
      }
    }
  }
}
</style>
