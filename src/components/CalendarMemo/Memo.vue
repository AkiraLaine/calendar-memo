<template>
  <div class='wrapper'>
    <div class='input-container'>
      <input class='input' :class='{"show": showInput}' type="text" v-model='memo' placeholder="Enter new memo..." ref='input' @keydown.enter='addMemo()' tabindex="0" @blur='showInput = false'>
      <div class='add' @click='fadeInInput()'>+</div>
    </div>
    <div class='date-container'>
      <div class='date'>{{ removeZero(dateInfo.date) }}</div>
      <div class='day'>{{ dateInfo.day}}</div>
    </div>
    <div class='memo-container'>
      <div class='memo' v-if='currentDateMemo' v-for='memo in currentDateMemo'>
        <div class='tick'>&bullet;</div>
        <div class='text'>{{ memo.name }}</div>
      </div>
      <div class='no-memo' v-if='!currentDateMemo'>No memo's for this day</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'memo',
  props: {
    dateInfo: Object,
    memos: Object
  },
  data () {
    return {
      showInput: false,
      memo: ''
    }
  },
  watch: {
    memos: {
      handler (val) {
        console.log(val)
      },
      deep: true
    }
  },
  methods: {
    removeZero (num) {
      if (num[0] === '0') return num.substring(1)
      else return num
    },
    fadeInInput () {
      this.showInput = true
      this.$refs.input.focus()
    },
    addMemo () {
      this.$emit('addMemo', this.memo)
      this.memo = ''
    }
  },
  computed: {
    currentDateMemo () {
      return this.memos[`${this.dateInfo.year}-${this.dateInfo.monthIndex}-${this.dateInfo.date}`] || null
    }
  }
}
</script>

<style scoped>
.wrapper {
  min-width: 345px;
  max-width: 345px;
  height: 480px;
  background-color: #E35D5B;
  position: absolute;
  top: -30px;
  right: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-shadow: 5px 10px 20px rgba(277,93,91,0.3);
  position: relative;
}
.input-container {
  position: absolute;
  top: 10px;
  width: 100%;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.input {
  background: none;
  outline: none;
  border: none;
  border-bottom: 1px solid #eee;
  width: 250px;
  padding: 5px;
  color: #eee;
  opacity: 0;
  transition: all 0.3s ease;
}
.input::placeholder {
  color: #eee;
}
.input.show {
  opacity: 1;
}
.add {
  font-size: 2.5em;
  color: #fff;
  cursor: pointer;
  position: relative;
  right: -15px;
}
.date-container {
  text-align: center;
  color: #fff;
  margin-bottom: 20px;
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
.memo-container {
  width: 80%;
  height: 100px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /*overflow-y: scroll;*/
}
.memo {
  display: flex;
  align-items: center;
  color: #eee;
  width: 100%;
  margin: 5px auto;
  cursor: pointer;
}
.memo:hover {
  opacity: 0.8;
}
.memo .text {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.memo .tick {
  margin-right: 10px;
  color: rgba(255,255,255,0.4);
  font-size: 1.5em;
}
.no-memo {
  color: #eee;
}
</style>
