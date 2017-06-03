<template>
  <div class='wrapper'>
    <div class='date-container'>
      <div class='date'>{{ removeZero(date.date) }}</div>
      <div class='day'>{{ date.day}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'memo',
  props: {
    date: Object
  },
  methods: {
    removeZero (num) {
      if (num[0] === '0') return num.substring(1)
      else return num
    }
  }
}
</script>

<style scoped>
.wrapper {
  width: 50%;
  height: 480px;
  background-color: #E35D5B;
  position: absolute;
  top: -40px;
  right: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.date-container {
  text-align: center;
  color: #fff;
}
.date {
  font-size: 6em;
}
.day {
  font-size: 1.1em;
  text-transform: uppercase;
  font-weight: 700;
  letter-spacing: 5px;
}
</style>
