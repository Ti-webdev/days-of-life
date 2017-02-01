<template lang="pug">
  .day(:class="className", :title="point")
</template>

<script>
export default {
  name: 'point',
  props: ['point', 'lived'],
  computed: {
    className () {
      if (this.point === this.lived) {
        return 'now'
      }
      if (this.point < this.lived) {
        return 'past'
      }
      return 'future'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus">
.day
  width 1em
  height 1em
  overflow hidden
  font-size 50%
  flex 0 0 auto
.past
  background #302E2E
.now
  background #FFE0BD
  animation blink-animation 1s steps(5, start) infinite
.future
  background #FFE0BD
@keyframes blink-animation {
  to {
    background #302E2E
  }
}
</style>
