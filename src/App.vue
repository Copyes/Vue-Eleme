<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
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
    <keep-alive>
      <router-view :seller="seller"/>
    </keep-alive>
  </div>
</template>

<script>
import { urlParse } from 'common/js/util'
import header from './components/header/index.vue'
const debug = process.env.NODE_ENV !== 'production'
const ERR_OK = 0

export default {
  data() {
    return {
      seller: {
        id: (() => {
          let queryParam = urlParse()
          return queryParam.id
        })()
      }
    }
  },
  created() {
    const url = debug ? '/api/seller' : 'http://ustbhuangyi.com/sell/api/seller'
    this.$http.get(url + '?id=' + this.seller.id).then(response => {
      response = response.data
      if (response.errno === ERR_OK) {
        this.seller = Object.assign({}, this.seller, response.data)
      }
    })
  },
  components: {
    'v-header': header
  }
}
</script>

<style lang="less">
@import './common/style/mixin.less';
@bs: 46.875rem;
.tab {
  display: flex;
  width: 100%;
  height: 80/@bs;
  line-height: 80/@bs;

  .border-1px(rgba(7, 17, 27, 0.1));

  .tab-item {
    flex: 1;
    text-align: center;

    & > a {
      display: block;
      color: rgb(77, 85, 93);
      font-size: 28/@bs;

      &.active {
        color: rgb(240, 20, 20);
      }
    }
  }
}
</style>
