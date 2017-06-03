<template>
  <div class='wrapper'>
    <calendar :date='date'></calendar>
    <memo :date='date'></memo>
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
      date: {
        date: moment().format('DD'),
        month: moment().format('MMMM'),
        day: moment().format('dddd'),
        year: moment().format('YYYY')
      }
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
