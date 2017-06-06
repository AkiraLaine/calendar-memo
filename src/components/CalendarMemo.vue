<template>
  <div class='wrapper'>
    <calendar :dateInfo='dateInfo' @changeDate='changeDate' :memos='memos'></calendar>
    <memo :dateInfo='dateInfo' :memos='memos' @addMemo='addMemo' @toggleMemoState='toggleMemoState' @deleteMemo='deleteMemo'></memo>
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
      },
      memos: {}
    }
  },
  created () {
    this.memos = JSON.parse(window.localStorage.getItem('memos')) || {}
  },
  methods: {
    changeDate (date) {
      this.dateInfo.date = date
      this.dateInfo.day = moment(`${this.dateInfo.year}-${this.dateInfo.monthIndex}-${this.dateInfo.date}`).format('dddd')
    },
    addMemo (memo) {
      let key = `${this.dateInfo.year}-${this.dateInfo.monthIndex}-${this.dateInfo.date}`
      this.memos[key] = this.memos[key] || []
      this.memos[key].push({
        name: memo,
        completed: false
      })
      this.memos = Object.assign({}, this.memos)
      window.localStorage.setItem('memos', JSON.stringify(this.memos))
    },
    toggleMemoState (memo) {
      memo.completed = !memo.completed
      window.localStorage.setItem('memos', JSON.stringify(this.memos))
    },
    deleteMemo (memo) {
      Object.keys(this.memos).forEach(date => {
        this.memos[date].forEach((m, i) => {
          if (m.name === memo.name) {
            this.memos[date].splice(i, 1)
          }
          if (this.memos[date].length === 0) delete this.memos[date]
        })
      })
      window.localStorage.setItem('memos', JSON.stringify(this.memos))
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
