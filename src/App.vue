<template>
  <hello></hello>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    Hello
  }
}
</script>

<style lang="stylus">
html
  margin 0
  padding 0
  font-size 15px
  width 100%
  height 100%
  display flex
  align-items center
  align-content center
  justify-content center
body
  margin 0
  padding 0

</style>
