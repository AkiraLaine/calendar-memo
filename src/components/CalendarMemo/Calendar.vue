<template>
  <div class='wrapper'>
    <div class='calendar'>
      <div class='month'>{{ date.month }}</div>
      <div class='weekdays'>
        <div class='day' :class='{"weekend": day.indexOf("S") > -1}' v-for='day in weekdays'>{{ day.toLowerCase() }}</div>
      </div>
      <div class='dates'>
        <div class="date" :class='{"today": isToday(addZero(date)), "faded": hasPassed(date)}' v-for='date in daysInMonth'>{{ addZero(date) }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'calendar',
  props: {
    date: Object
  },
  data () {
    return {
      moment,
      weekdays: ['Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa', 'Su']
    }
  },
  computed: {
    daysInMonth () {
      return this.moment(`${this.date.year}-${this.date.month}`).daysInMonth()
    }
  },
  methods: {
    addZero (num) {
      if (Number(num) < 10) return `0${num}`
      else return num
    },
    isToday (date) {
      let dateArray = new Date().toString().split(' ')
      if (this.date.month.indexOf(dateArray[1]) > -1 && date === dateArray[2]) {
        return true
      }
    },
    hasPassed (date) {
      let currentDate = Number(new Date().toString().split(' ')[2])
      if (Number(date) < currentDate) return true
    }
  }
}
</script>

<style scoped>
.wrapper {
  width: 48%;
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.calendar  {
  margin: 0 auto;
  width: 80%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.month {
  font-weight: 700;
  letter-spacing: 5px;
  color: #333;
  text-transform: uppercase;
  font-size: 1.1em;
  margin-bottom: 20px;
}
.weekdays {
  width: 100%;
  display: flex;
  margin-bottom: 20px;
}
.day {
  color: #333;
  width: 35px;
  text-align: center;
  margin-right: 3px;
}
.day.weekend {
  color: #fa8072;
}
.dates {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  line-height: 35px;
}
.date {
  font-size: 1.1em;
  color: #333;
  width: 35px;
  text-align: center;
  margin-right: 3px;
  position: relative;
  z-index: 10;
}
.date.today {
  color: #fff;
}
.date.today::after {
  content: '';
  width: 30px;
  height: 30px;
  border-radius: 50%;
  position: absolute;
  top: 2px;
  left: 3px;
  background-color: #E35D5B;
  z-index: -1;
}
.date.faded {
  color: #ddd;
}
</style>
