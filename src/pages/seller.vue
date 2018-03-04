<template>
  <div class="seller" ref="seller">
    <div class="seller-wrapper">
      <div class="summary">
        <h1 class="title">{{seller.name}}</h1>
        <div class="desc border-1px">
          <star :size="36" :score="seller.score"></star>
          <span class="text">({{seller.ratingCount}})</span>
          <span class="text">月售{{seller.sellCount}}单</span>
        </div>
        <ul class="remark">
          <li class="block">
            <h2>起送价</h2>
            <div class="content">
              <span class="stress">{{seller.minPrice}}</span>元
            </div>
          </li>
          <li class="block">
            <h2>商家配送</h2>
            <div class="content">
              <span class="stress">{{seller.deliveryPrice}}</span>元
            </div>
          </li>
          <li class="block">
            <h2>平均配送时间</h2>
            <div class="content">
              <span class="stress">{{seller.deliveryTime}}</span>分钟
            </div>
          </li>
        </ul>
        <div class="favorite" @click="toggleFavorite">
          <span class="icon-favorite" :class="{'active':favorite}"></span>
          <span class="text">{{favoriteText}}</span>
        </div>
      </div>
      <div class="activity">
        <h1 class="title">公告与活动</h1>
        <div class="content-wrapper border-1px">
          <p class="content">{{seller.bulletin}}</p>
        </div>
        <ul v-if="seller.supports" class="supports">
          <li class="support-item border-1px" v-for="(item,index) in seller.supports" :key="index">
            <span class="icon" :class="classMap[seller.supports[index].type]"></span>
            <span class="text">{{seller.supports[index].description}}</span>
          </li>
        </ul>
      </div>
      <div class="pics">
        <h1 class="title">商家实景</h1>
        <div class="pic-wrapper" ref="picWrapper">
          <ul class="pic-list" ref="picList">
            <li class="pic-item" v-for="(pic, index) in seller.pics" :key="index">
              <img :src="pic" width="240" height="180">
            </li>
          </ul>
        </div>
      </div>
      <div class="info">
        <h1 class="title border-1px">商家信息</h1>
        <ul>
          <li class="info-item" v-for="(info, index) in seller.infos" :key="index">{{info}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
import star from '../components/star/index.vue'
import BScroll from 'better-scroll'

export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      favorite: false
    }
  },
  watch: {
    seller() {
      this.$nextTick(() => {
        this._initScroll()
        this._initPics()
      })
    }
  },
  mounted() {
    this.$nextTick(() => {
      this._initScroll()
      this._initPics()
    })
  },
  computed: {
    favoriteText() {
      return this.favorite ? '已收藏' : '收藏'
    }
  },
  created() {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  methods: {
    toggleFavorite() {},
    _initScroll() {
      if (!this.scroll) {
        this.scroll = new BScroll(this.$refs.seller, {
          click: true
        })
      } else {
        this.scroll.refresh()
      }
    },
    _initPics() {
      if (this.seller.pics) {
        let picWidth = 240
        let margin = 12
        let width = (picWidth + margin) * this.seller.pics.length - margin
        this.$refs.picList.style.width = width + 'px'
        this.$nextTick(() => {
          if (!this.picScroll) {
            this.picScroll = new BScroll(this.$refs.picWrapper, {
              scrollX: true,
              eventPassthrough: 'vertical'
            })
          } else {
            this.picScroll.refresh()
          }
        })
      }
    }
  },
  components: {
    star
  }
}
</script>
<style lang="less">
@import '../common/style/mixin.less';
.bg-image(@path) {
  background-image: url('@{path}@2x.png');
}
@bs: 46.875rem;
.seller {
  position: absolute;
  top: 352/@bs;
  bottom: 0;
  left: 0;
  overflow: hidden;
  width: 100%;
  background-color: #f3f5f7;
  .summary {
    position: relative;
    padding: 36/@bs;
    border-bottom: 1px solid rgba(7, 17, 27, 0.1);
    background-color: #fff;
    .title {
      margin-bottom: 16/@bs;
      color: rgb(7, 17, 27);
      font-size: 28/@bs;
      line-height: 1;
    }
    .desc {
      padding-bottom: 36/@bs;
      font-size: 0;

      .border-1px(rgba(7, 17, 27, 0.1));
      .star {
        display: inline-block;
        margin-right: 16/@bs;
      }

      .text {
        display: inline-block;
        margin-right: 24/@bs;
        color: rgb(77, 85, 93);
        vertical-align: top;
        font-size: 24/@bs;
        line-height: 36/@bs;
      }
    }
    .remark {
      display: flex;
      padding-top: 36/@bs;

      .block {
        flex: 1;
        border-right: 1px solid rgba(7, 17, 27, 0.1);
        text-align: center;

        &:last-child {
          border: none;
        }

        h2 {
          margin-bottom: 8/@bs;
          color: rgb(147, 153, 159);
          font-size: 20/@bs;
          line-height: 1;
        }

        .content {
          color: rgb(7, 17, 27);
          font-size: 20/@bs;
          line-height: 48/@bs;

          .stress {
            font-size: 48/@bs;
          }
        }
      }
    }
    .favorite {
      position: absolute;
      top: 36/@bs;
      right: 22/@bs;
      width: 100/@bs;
      text-align: center;
      font-size: 0;
      .icon-favorite {
        display: block;
        margin-bottom: 16/@bs;
        color: #d4d6d9;
        font-size: 48/@bs;
        line-height: 1;

        &.active {
          color: rgb(240, 20, 20);
        }
      }

      .text {
        color: rgb(77, 85, 93);
        font-size: 24/@bs;
        line-height: 1;
      }
    }
  }
  .activity {
    margin-top: 36/@bs;
    padding: 36/@bs 36/@bs 0 36/@bs;
    background-color: #fff;
    .title {
      margin-bottom: 16/@bs;
      color: rgb(7, 17, 27);
      font-size: 28/@bs;
      line-height: 1;
    }

    .content-wrapper {
      padding: 0 24/@bs 32/@bs;

      .border-1px(rgba(7, 17, 27, 0.1));

      .content {
        color: rgb(240, 20, 20);
        font-size: 24/@bs;
        line-height: 2;
      }
    }

    .supports {
      .support-item {
        padding: 32/@bs 24/@bs;
        font-size: 0;

        .border-1px(rgba(7, 17, 27, 0.1));

        &:last-child {
          border: none;
        }
      }

      .icon {
        display: inline-block;
        margin-right: 12/@bs;
        width: 32/@bs;
        height: 32/@bs;
        background-size: 32/@bs 32/@bs;
        background-repeat: no-repeat;
        vertical-align: top;

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
        color: rgb(7, 17, 27);
        font-size: 24/@bs;
        line-height: 32/@bs;
      }
    }
  }
  .pics {
    margin-top: 36/@bs;
    padding: 36/@bs;
    background-color: #fff;
    .title {
      margin-bottom: 24/@bs;
      color: rgb(7, 17, 27);
      font-size: 28/@bs;
      line-height: 1;
    }

    .pic-wrapper {
      overflow: hidden;
      width: 100%;
      white-space: nowrap;

      .pic-list {
        font-size: 0;

        .pic-item {
          display: inline-block;
          margin-right: 12/@bs;
          width: 240/@bs;
          height: 180/@bs;

          &:last-child {
            margin: 0;
          }
        }
      }
    }
  }
  .info {
    margin-top: 36/@bs;
    padding: 36/@bs 36/@bs 0 36/@bs;
    background-color: #fff;
    color: rgb(7, 17, 27);

    .title {
      padding-bottom: 24/@bs;
      font-size: 28/@bs;
      line-height: 1;

      .border-1px(rgba(7, 17, 27, 0.1));
    }

    .info-item {
      padding: 32/@bs 24/@bs;
      font-size: 24/@bs;
      line-height: 1.3;

      .border-1px(rgba(7, 17, 27, 0.1));

      &:last-child {
        border: none;
      }
    }
  }
}
</style>
