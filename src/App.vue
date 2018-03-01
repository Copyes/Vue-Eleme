<template>
  <div id="app">
    <v-header></v-header>
    <router-view/>
  </div>
</template>

<script>
import header from './components/header/index.vue'

export default {
  data() {
    return {}
  },
  components: {
    'v-header': header
  }
}
</script>

<style lang="less">

</style>
