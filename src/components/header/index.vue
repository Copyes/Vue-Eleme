<template>
  <div class="header">
    <div class="header-container">
      <div class="avatar">
        <img src="http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg" alt="">
      </div>
      <div class="content">
        <p class="title">粥品香坊（回龙观）</p>
        <p class="desc">蜂鸟专送/38分钟送达</p>
        <p class="support"></p>
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
    padding: 32/@bs;
    .avatar {
      width: 120/@bs;
      height: 120/@bs;
      img {
        width: 100%;
        height: 100%;
      }
    }
    .content {
    }
  }
  &-notice {
    position: relative;
    overflow: hidden;
    padding: 0 12/@bs;
    height: 48/@bs;
    background: rgba(7, 17, 27, 0.2);
    text-overflow: ellipsis;
    white-space: nowrap;
    font-size: 0;
    line-height: 48/@bs;
    .icon-notice {
      display: inline-block;
      width: 44/@bs;
      height: 48/@bs;
      background: url('./bulletin@2x.png') center no-repeat;
      background-size: 44/@bs 28/@bs;
      vertical-align: middle;
    }
    .notice-desc {
      margin-left: 8/@bs;
      vertical-align: middle;
      font-size: 26/@bs;
    }
    .icon-keyboard_arrow_right {
      position: absolute;
      top: 8/@bs;
      right: 8/@bs;
      font-size: 30/@bs;
    }
  }
}
</style>

