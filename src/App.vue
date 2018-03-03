<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <router-view/>
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
      console.log(response)
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

</style>
