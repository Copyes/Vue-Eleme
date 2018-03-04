<template>
  <div class="ratings" ref="ratings">
    <div class="ratings-content">
      <div class="summary">
        <div class="summary-left">
          <h1 class="score">{{seller.score}}</h1>
          <p class="title">综合评分</p>
          <p class="rank">高于周边商家{{seller.rankRate}}%</p>
        </div>
        <div class="summary-right">
          <div class="score-wrapper">
            <span class="title">服务态度</span>
            <star :size="36" :score="seller.serviceScore"></star>
            <span class="score">{{seller.serviceScore}}</span>
          </div>
          <div class="score-wrapper">
            <span class="title">商品评分</span>
            <star :size="36" :score="seller.foodScore"></star>
            <span class="score">{{seller.foodScore}}</span>
          </div>
          <div class="delivery-wrapper">
            <span class="title">送达时间</span>
            <span class="delivery">{{seller.deliveryTime}}分钟</span>
          </div>
        </div>
      </div>
      <rating-selection @select="selectRating" @toggle="toggleContent" :ratings="ratings" :selectType="selectType" :onlyContent="onlyContent" ></rating-selection>
      <div class="comments">
        <ul>
          <li v-for="(rating, index) in ratings" v-show="needShow(rating.rateType, rating.text)" :key="index" class="rating-item">
            <div class="avatar">
              <img width="56" height="56" :src="rating.avatar">
            </div>
            <div class="content">
              <h1 class="name">{{rating.username}}</h1>
              <div class="star-wrapper">
                <star :size="24" :score="rating.score"></star>
                <span class="delivery" v-show="rating.deliveryTime">{{rating.deliveryTime}}</span>
              </div>
              <p class="text">{{rating.text}}</p>
              <div class="recommend" v-show="rating.recommend && rating.recommend.length">
                <span class="icon-thumb_up"></span>
                <span class="item" v-for="(item,index) in rating.recommend" :key="index">{{item}}</span>
              </div>
              <div class="time">
                {{rating.rateTime | formatDate}}
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
import star from '../components/star/index.vue'
import RatingsSelection from '../components/ratings-selection/index.vue'
import BScroll from 'better-scroll'
import { formatDate } from 'common/js/util.js'

const ALL = 2
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
      ratings: [],
      selectType: ALL,
      onlyContent: true
    }
  },
  created() {
    this.getData()
  },
  methods: {
    getData() {
      const url = debug
        ? '/api/ratings'
        : 'http://ustbhuangyi.com/sell/api/ratings'
      this.$http
        .get(url)
        .then(res => {
          let resp = res.data
          if (resp.errno === ERR_OK) {
            this.ratings = resp.data
            this.$nextTick(() => {
              this.scroll = new BScroll(this.$refs.ratings, {
                click: true
              })
            })
          }
        })
        .catch(err => {
          console.log(err)
        })
    },
    selectRating(type) {
      this.selectType = type
      this.$nextTick(() => {
        this.scroll.refresh()
      })
    },
    toggleContent() {
      this.onlyContent = !this.onlyContent
      this.$nextTick(() => {
        this.scroll.refresh()
      })
    },
    needShow(type, text) {
      if (this.onlyContent && !text) {
        return false
      }
      if (this.selectType === ALL) {
        return true
      } else {
        return type === this.selectType
      }
    }
  },
  filters: {
    formatDate(time) {
      let date = new Date(time)
      return formatDate(date, 'yyyy-MM-dd hh:mm')
    }
  },
  components: {
    star,
    'rating-selection': RatingsSelection
  }
}
</script>
<style lang="less">
@bs: 46.875rem;
.ratings {
  position: absolute;
  top: 352/@bs;
  bottom: 0;
  left: 0;
  overflow: hidden;
  width: 100%;
  background-color: #f3f5f7;
  .summary {
    display: flex;
    margin-bottom: 36/@bs;
    padding: 36/@bs 0;
    border-bottom: 1px solid rgba(7, 17, 27, 0.1);
    background-color: #fff;
    &-left {
      flex: 0 0 274/@bs;
      padding: 12/@bs 0;
      width: 274/@bs;
      border-right: 1px solid rgba(7, 17, 27, 0.1);
      text-align: center;
      .score {
        margin-bottom: 12/@bs;
        color: rgb(255, 153, 0);
        font-size: 48/@bs;
        line-height: 56/@bs;
      }

      .title {
        margin-bottom: 16/@bs;
        color: rgb(7, 17, 27);
        font-size: 24/@bs;
        line-height: 1;
      }

      .rank {
        color: rgb(147, 153, 159);
        font-size: 22/@bs;
        line-height: 1;
      }
    }
    &-right {
      flex: 1;
      padding: 12/@bs 0 12/@bs 48/@bs;
      .score-wrapper {
        margin-bottom: 16/@bs;
        font-size: 0;

        .title {
          display: inline-block;
          color: rgb(7, 17, 27);
          vertical-align: top;
          font-size: 24/@bs;
          line-height: 1.5;
        }

        .star {
          display: inline-block;
          margin: 0 24/@bs;
          vertical-align: top;
        }

        .score {
          display: inline-block;
          color: rgb(255, 153, 0);
          vertical-align: top;
          font-size: 24/@bs;
          line-height: 1.5;
        }
      }
      .delivery-wrapper {
        font-size: 0;

        .title {
          color: rgb(7, 17, 27);
          font-size: 24/@bs;
          line-height: 1.5;
        }

        .delivery {
          margin-left: 24/@bs;
          color: rgb(147, 153, 159);
          font-size: 24/@bs;
        }
      }
    }
  }
  .comments {
    padding: 0 36/@bs;
    background-color: #fff;
    .rating-item {
      display: flex;
      padding: 36/@bs 0;
      border-bottom: 1px solid rgba(7, 17, 27, 0.1);

      .avatar {
        flex: 0 0 56/@bs;
        margin-right: 24/@bs;
        width: 56/@bs;

        img {
          border-radius: 50%;
        }
      }

      .content {
        position: relative;
        flex: 1;

        .name {
          margin-bottom: 8/@bs;
          color: rgb(7, 17, 27);
          font-size: 22/@bs;
          line-height: 1.2;
        }

        .star-wrapper {
          margin-bottom: 12/@bs;
          font-size: 0;

          .star {
            display: inline-block;
            margin-right: 12/@bs;
            vertical-align: top;
          }

          .delivery {
            display: inline-block;
            color: rgb(147, 153, 159);
            vertical-align: top;
            font-size: 24/@bs;
            line-height: 1.2;
          }
        }

        .text {
          margin-bottom: 16/@bs;
          color: rgb(7, 17, 27);
          font-size: 24/@bs;
          line-height: 1.5;
        }

        .recommend {
          font-size: 0;
          line-height: 32/@bs;

          .icon-thumb_up,
          .item {
            display: inline-block;
            margin: 0 16/@bs 8/@bs 0;
            font-size: 22/@bs;
          }

          .icon-thumb_up {
            color: rgb(0, 160, 220);
          }

          .item {
            padding: 0 12/@bs;
            border: 1px solid rgba(7, 17, 27, 0.1);
            border-radius: 1px;
            background: #fff;
            color: rgb(147, 153, 159);
          }
        }

        .time {
          position: absolute;
          top: 0;
          right: 0;
          color: rgb(147, 153, 159);
          font-size: 22/@bs;
          line-height: 1.2;
        }
      }
    }
  }
}
</style>
