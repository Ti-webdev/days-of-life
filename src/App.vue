<template lang="pug">
  .root
    h1 {{percent}}%
    .days
      Day(v-for="d in days", :day="d", :lived="lived")
</template>

<script>
import Day from './components/Day'
import moment from 'moment'
import {CronJob} from 'cron'

export default {
  name: 'app',
  data () {
    return {
      birthday: moment('1985-03-13T00:00:01'),
      now: moment()
    }
  },
  methods: {
    updateNow () {
      this.now = moment()
    }
  },
  created () {
    /* eslint-disable no-new */
    new CronJob('0 0 0 * * *', () => this.updateNow(), null, true)
  },
  computed: {
    last () {
      return moment(this.birthday).add(60, 'years')
    },
    days () {
      return this.last.diff(this.birthday, 'days')
    },
    lived () {
      return this.now.diff(this.birthday, 'days')
    },
    percent () {
      return Number(100 * this.lived / this.days).toFixed(1)
    }
  },
  components: {
    Day
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
body
  flex 1 0 auto
  margin 0
  padding 0
  width 100%
  display flex
.root
  flex 0 1 auto
  width 100%
  display flex
  flex-direction column
  align-items center
  align-content center
  justify-content center
h1
  text-align center
  flex 0 0 auto
.days
  flex 0 1 auto
  display flex
  flex-wrap wrap
  //align-items center
  //align-content center
  //justify-content center
</style>
