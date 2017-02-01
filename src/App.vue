<template lang="pug">
  .root
    h1 {{percent}}%
    .radio
      label
        input(type="radio" value="weeks" v-model="grade")
        = ' Weeks'
      label
        input(type="radio" value="days" v-model="grade")
        = ' Days'
    .points(:class="grade")
      Point(v-for="point in points", :point="point", :lived="lived")
</template>

<script>
import Point from './components/Point'
import moment from 'moment'
import {CronJob} from 'cron'

export default {
  name: 'app',
  data () {
    return {
      birthday: moment('1985-03-13T00:00:01'),
      now: moment(),
      grade: 'weeks'
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
    points () {
      return this.last.diff(this.birthday, this.grade)
    },
    lived () {
      return this.now.diff(this.birthday, this.grade)
    },
    percent () {
      return Number(100 * this.lived / this.points).toFixed(1)
    }
  },
  components: {
    Point
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
  @media screen and (max-width: 800px) , screen and (max-height: 800px) {
    font-size 8px
  }
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
.points
  flex 0 1 auto
  display flex
  flex-wrap wrap
  max-width 1024px
  //align-items center
  //align-content center
  //justify-content center
.weeks
  font-size 200%
</style>
