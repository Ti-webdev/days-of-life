<template lang="pug">
  div
    h1 {{percent}}%
    .days
      Day(v-for="d in days", :day="d", :lived="lived")
</template>

<script>
import Day from './Day'
import moment from 'moment'
import {CronJob} from 'cron'
export default {
  name: 'hello',
  data () {
    return {
      birthday: moment('1985.03.13 00:00:01'),
      now: moment()
    }
  },
  created () {
    /* eslint-disable no-new */
    new CronJob('0 0 0 * * *', () => {
      this.now = moment()
    }, null,
      true
    )
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
h1
  text-align: center
.days
  flex 0 0 auto
  display flex
  flex-wrap wrap
  align-items center
  align-content center
  justify-content center
  margin-left 1px
  margin-top 1px
</style>
