<template>
  <div class="star" :class="starType">
    <span class="star-item" v-for="(item, index) in itemsClasses" :key="index" :class="item"></span>
  </div>
</template>
<script>
const LENGTH = 5
const CLS_ON = 'on'
const CLS_OFF = 'off'
const CLS_HALF = 'half'

export default {
  props: {
    size: {
      type: Number
    },
    score: {
      type: Number
    }
  },
  computed: {
    starType() {
      return `star-${this.size}`
    },
    itemsClasses() {
      let result = []
      let score = Math.floor(this.score * 2) / 2
      let hasDecimal = score % 1 !== 0
      let integer = Math.floor(score)

      for (let i = 0; i < integer; i++) {
        result.push(CLS_ON)
      }
      hasDecimal && result.push(CLS_HALF)

      while (result.length < LENGTH) {
        result.push(CLS_OFF)
      }
      return result
    }
  }
}
</script>
<style lang="less">
@bs: 46.875rem;
.bg-image(@path) {
  background-image: url('@{path}@3x.png');
}
.star {
  font-size: 0;
  .star-item {
    display: inline-block;
    background-repeat: no-repeat;
  }
  &.star-48 {
    .star-item {
      margin-right: 44/@bs;
      width: 40/@bs;
      height: 40/@bs;
      background-size: 40/@bs 40/@bs;

      &:last-child {
        margin-right: 0;
      }

      &.on {
        .bg-image('star48_on');
      }

      &.half {
        .bg-image('star48_half');
      }

      &.off {
        .bg-image('star48_off');
      }
    }
  }
  &.star-36 {
    .star-item {
      margin-right: 12/@bs;
      width: 30/@bs;
      height: 30/@bs;
      background-size: 30/@bs 30/@bs;

      &:last-child {
        margin-right: 0;
      }

      &.on {
        .bg-image('star36_on');
      }

      &.half {
        .bg-image('star36_half');
      }

      &.off {
        .bg-image('star36_off');
      }
    }
  }

  &.star-24 {
    .star-item {
      margin-right: 6/@bs;
      width: 20/@bs;
      height: 20/@bs;
      background-size: 20/@bs 20/@bs;

      &:last-child {
        margin-right: 0;
      }

      &.on {
        .bg-image('star24_on');
      }

      &.half {
        .bg-image('star24_half');
      }

      &.off {
        .bg-image('star24_off');
      }
    }
  }
}
</style>

