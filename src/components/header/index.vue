<template>
  <div class="header">
    <div class="header-container">
      <div class="avatar">
        <img src="http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg" alt="">
      </div>
      <div class="content">
        <p class="title">粥品香坊（回龙观）</p>
        <p class="desc">蜂鸟专送/38分钟送达</p>
        <div class="support">
          <span class="icon decrease"></span>
          <span class="text">在线支付满28减5</span>
        </div>
      </div>
    </div>
    <div class="header-notice">
      <span class="icon-notice"></span>
      <span class="notice-desc">粥品香坊其烹饪粥料的秘方源于中国千年古法，在融和现代制作工艺，由世界烹饪大师屈浩先生领衔研发。坚守纯天然、0添加的良心品质深得消费者青睐，发展至今成为粥类的引领品牌。是2008年奥运会和2013年园博会指定餐饮服务商。</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {}
  }
}
</script>
<style lang="less">
@import url('../../common/style/mixin.less');
@bs: 46.875rem;
.header {
  position: relative;
  overflow: hidden;
  background: rgba(71, 104, 138, 0.5);
  color: #fff;
  &-container {
    position: relative;
    padding: 32/@bs;
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
}
</style>
