<template>
  <div id="app">
    <calendar-memo></calendar-memo>
  </div>
</template>

<script>
import CalendarMemo from './components/CalendarMemo'

export default {
  name: 'app',
  components: {
    CalendarMemo
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Inconsolata:400,700');

* {
  margin: 0;
  padding: 0;
  user-select: none;
}
#app {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Inconsolata';
  background-color: #fcfcfc;
}
</style>
