<template lang="pug">
  .day(:class="className", :title="day")
</template>

<script>
export default {
  name: 'day',
  props: ['day', 'lived'],
  computed: {
    className () {
      if (this.day === this.lived) {
        return 'today'
      }
      if (this.day < this.lived) {
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
.today
  background #FFE0BD
  animation blink-animation 1s steps(2, start) infinite
.future
  background #FFE0BD
@keyframes blink-animation {
  to {
    background #302E2E
  }
}
</style>
