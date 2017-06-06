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
      <div class='memo' :class='{"completed": memo.completed}' v-if='currentDateMemo' v-for='memo in currentDateMemo' @click='toggleMemoState(memo)'>
        <div class='tick'>&bullet;</div>
        <div class='text'>{{ memo.name }}</div>
        <div class='delete' @click.stop='deleteMemo(memo)'><span style="margin-top:-2px">x</span></div>
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
      if (this.memo) {
        this.$emit('addMemo', this.memo)
        this.memo = ''
      }
    },
    toggleMemoState (memo) {
      this.$emit('toggleMemoState', memo)
    },
    deleteMemo (memo) {
      this.$emit('deleteMemo', memo)
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
  box-shadow: 5px 10px 20px rgba(277,93,91,0.3);
  position: relative;
}
.input-container {
  width: 100%;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 10px;
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
  margin: 20px 0;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
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
  min-height: 170px;
  max-height: 170px;
  margin: 15px auto;
  overflow: hidden;
  text-align: center;
}
.memo-container:hover {
  overflow-y: auto;
}
.memo-container::-webkit-scrollbar {
  width: 5px;
}
.memo-container::-webkit-scrollbar-track {
  background: transparent;
}
.memo-container::-webkit-scrollbar-thumb {
  background-color: rgba(255,255,255,0.4);
  border-radius: 10px;
}
.memo-container .title {
  color: #eee;
  margin: 5px 0;
}
.memo {
  display: flex;
  align-items: center;
  color: #eee;
  width: 90%;
  cursor: pointer;
  position: relative;
}
.memo .text {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-width: 80%;
}
.memo .tick {
  margin-right: 10px;
  color: rgba(255,255,255,0.4);
  font-size: 1.5em;
}
.memo .delete {
  margin-left: auto;
  color: #E35D5B;
  background-color: #fff;
  width: 15px;
  height: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  font-size: 0.9em;
  opacity: 0.8;
  visibility: hidden;
}
.memo:hover .delete {
  visibility: visible;
}
.memo .delete:hover {
  opacity: 1;
}
.memo.completed .tick, .memo.completed .text {
  opacity: 0.4;
}
.memo.completed .text {
  text-decoration: line-through;
}
.no-memo {
  color: #eee;
}
</style>
