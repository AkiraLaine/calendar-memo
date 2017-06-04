<template>
  <div class='wrapper'>
    <calendar :dateInfo='dateInfo' @changeDate='changeDate'></calendar>
    <memo :dateInfo='dateInfo'></memo>
  </div>
</template>

<script>
import Calendar from './CalendarMemo/Calendar'
import Memo from './CalendarMemo/Memo'
import moment from 'moment'

export default {
  components: {
    Calendar,
    Memo
  },
  name: 'calendar-memo',
  data () {
    return {
      dateInfo: {
        date: moment().format('DD'),
        month: moment().format('MMMM'),
        monthIndex: moment().format('MM'),
        day: moment().format('dddd'),
        year: moment().format('YYYY')
      }
    }
  },
  methods: {
    changeDate (date) {
      this.dateInfo.date = date
      this.dateInfo.day = moment(`${this.dateInfo.year}-${this.dateInfo.monthIndex}-${this.dateInfo.date}`).format('dddd')
    }
  }
}
</script>

<style scoped>
.wrapper {
  width: 700px;
  height: 400px;
  background-color: #fff;
  box-shadow: 0 7px 15px rgba(0,0,0,0.2);
  display: flex;
  position: relative;
}
</style>
