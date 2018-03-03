<template>
  <div class="header">
    <div class="header-container">
      <div class="avatar">
        <img :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <p class="title">{{seller.name}}</p>
        <p class="desc">{{seller.description}}/{{seller.deliveryTime}}分钟送达</p>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
    </div>
    <div class="header-notice" @click="showDetail = true">
      <span class="icon-notice"></span>
      <span class="notice-desc">粥品香坊其烹饪粥料的秘方源于中国千年古法，在融和现代制作工艺，由世界烹饪大师屈浩先生领衔研发。坚守纯天然、0添加的良心品质深得消费者青睐，发展至今成为粥类的引领品牌。是2008年奥运会和2013年园博会指定餐饮服务商。</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="header-background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <transition name="fade">
      <div v-show="showDetail" class="header-detail">
          <div class="detail-wrapper">
            <div class="wrapper-main">
              <h1 class="name">{{seller.name}}</h1>
              <div class="stars-box">
                <star :size="48" :score="seller.score"></star>
              </div>
              <div class="title">
                <div class="line"></div>
                <div class="text">优惠信息</div>
                <div class="line"></div>
              </div>
              <ul v-if="seller.supports" class="supports">
                <li class="support-item" v-for="(item,index) in seller.supports" :key="index">
                  <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                  <span class="text">{{seller.supports[index].description}}</span>
                </li>
              </ul>
              <div class="title">
                <div class="line"></div>
                <div class="text">商家公告</div>
                <div class="line"></div>
              </div>
              <div class="bulletin">
                <p class="content">{{seller.bulletin}}</p>
              </div>
            </div>
            <div class="wrapper-footer" @click="showDetail = false">
              <i class="icon-close"></i>
            </div>
          </div>
      </div>
    </transition>
    
  </div>
</template>
<script>
import star from '../star/index.vue'
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      showDetail: false,
      score: 4.5
    }
  },
  created() {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  components: {
    star
  }
}
</script>
<style lang="less">
@import url('../../common/style/mixin.less');
@bs: 46.875rem;
.bg-image(@path) {
  background-image: url('@{path}@2x.png');
}
.header {
  position: relative;
  overflow: hidden;
  background: rgba(71, 104, 138, 0.5);
  color: #fff;
  &-container {
    position: relative;
    padding: 48/@bs 32/@bs;
    font-size: 0;
    .avatar {
      display: inline-block;
      width: 120/@bs;
      height: 120/@bs;
      img {
        width: 100%;
        height: 100%;
        border-radius: 4/@bs;
      }
    }
    .content {
      display: inline-block;
      overflow: hidden;
      margin-left: 32/@bs;
      .title {
        margin-bottom: 16/@bs;
        padding-left: 68/@bs;
        height: 36/@bs;
        background: url('./brand@2x.png') no-repeat;
        font-size: 36/@bs;
      }
      .desc {
        margin-bottom: 16/@bs;
        font-size: 24/@bs;
        line-height: 1;
      }
      .support {
        .icon {
          display: inline-block;
          margin-right: 8/@bs;
          width: 24/@bs;
          height: 24/@bs;
          background-size: 24/@bs 24/@bs;
          background-repeat: no-repeat;
          vertical-align: top;

          &.decrease {
            background-image: url('./decrease_2@2x.png');
          }

          &.discount {
            background-image: url('./discount_2@2x.png');
          }

          &.guarantee {
            background-image: url('./guarantee_2@2x.png');
          }

          &.invoice {
            background-image: url('./invoice_2@2x.png');
          }

          &.special {
            background-image: url('./special_2@2x.png');
          }
        }

        .text {
          font-size: 20/@bs;
          line-height: 24/@bs;
        }
      }
    }
  }
  &-notice {
    position: relative;
    overflow: hidden;
    padding: 0 44/@bs 0 24/@bs;
    height: 56/@bs;
    background: rgba(7, 17, 27, 0.2);
    text-overflow: ellipsis;
    white-space: nowrap;
    font-size: 0;
    line-height: 56/@bs;
    .icon-notice {
      display: inline-block;
      width: 44/@bs;
      height: 56/@bs;
      background: url('./bulletin@2x.png') center no-repeat;
      background-size: 44/@bs 24/@bs;
      vertical-align: middle;
    }
    .notice-desc {
      margin: 0 8/@bs;
      vertical-align: middle;
      font-size: 24/@bs;
    }
    .icon-keyboard_arrow_right {
      position: absolute;
      top: 8/@bs;
      right: 16/@bs;
      font-size: 40/@bs;
    }
  }
  &-background {
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    width: 100%;
    height: 100%;
    filter: blur(20/@bs);
  }
  &-detail {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 100;
    overflow: auto;
    width: 100%;
    height: 100%;
    background: rgba(7, 17, 27, 0.8);
    opacity: 1;

    &.fade-enter-active,
    &.fade-leave-active {
      transition: all 0.5s;
    }

    &.fade-enter,
    &.fade-leave-active {
      background: rgba(7, 17, 27, 0);
      opacity: 0;
    }
    .detail-wrapper {
      min-height: 100%;
      width: 100%;
      .wrapper-main {
        padding-top: 128/@bs;
        padding-bottom: 128/@bs;
        .name {
          text-align: center;
          font-weight: 700;
          font-size: 32/@bs;
          line-height: 1;
        }
        .stars-box {
          margin-top: 36/@bs;
          padding: 4/@bs 0;
          text-align: center;
        }
        .title {
          display: flex;
          margin: 56/@bs auto 48/@bs auto;
          width: 80%;

          .line {
            position: relative;
            top: -12/@bs;
            flex: 1;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
          }

          .text {
            padding: 0 24/@bs;
            font-weight: 700;
            font-size: 28/@bs;
          }
        }
        .supports {
          margin: 0 auto;
          width: 80%;

          .support-item {
            margin-bottom: 24/@bs;
            padding: 0 24/@bs;
            font-size: 0;

            &:last-child {
              margin-bottom: 0;
            }

            .icon {
              display: inline-block;
              margin-right: 24/@bs;
              width: 32/@bs;
              height: 32/@bs;
              background-size: 32/@bs 32/@bs;
              background-repeat: no-repeat;
              vertical-align: top;

              &.decrease {
                .bg-image('decrease_2');
              }

              &.discount {
                .bg-image('discount_2');
              }

              &.guarantee {
                .bg-image('guarantee_2');
              }

              &.invoice {
                .bg-image('invoice_2');
              }

              &.special {
                .bg-image('special_2');
              }
            }

            .text {
              font-size: 24/@bs;
              line-height: 32/@bs;
            }
          }
        }
        .bulletin {
          margin: 0 auto;
          width: 80%;

          .content {
            padding: 0 24/@bs;
            font-size: 24/@bs;
            line-height: 2;
          }
        }
      }
      .wrapper-footer {
        margin: 0 auto;
        width: 64/@bs;
        height: 64/@bs;
        font-size: 64/@bs;
      }
    }
  }
}
</style>
