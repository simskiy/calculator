<template lang="pug">
  div.calculator
    input.input(type="text" v-model="value")
    span.buff hello
    div.wrapper
      div.row(v-for="row in buttons")
        div.cell(v-for="cell in row")
          button.btn(v-html="cell.title" @click="inputBtn(cell)")
</template>

<script>
import btns from './btns.js'
const { evaluate } = require('mathjs')

export default {
  data () {
    return {
      buttons: btns,
      value: ''
    }
  },
  methods: {
    inputBtn (btn) {
      /* eslint-disable */
      if (btn.type === 'number' || 'operator') this.value += btn.value
      if (btn.type === 'cancel') this.value = ''
      if (btn.type === 'enter') this.value = evaluate(this.value)
      console.log(this.value)
      /* eslint-enable */
    }
  }
}
</script>

<style lang="scss" scoped>

html {
  font-size: 16px;
}

.calculator {
  display: inline-block;
  position: relative;
  border: 1px solid black;
  border-radius: 5px;
  padding: 0.3rem;
}

.wrapper {
  display: table;
}

.input {
  box-sizing: border-box;
  width: calc(100% - 0.4rem);
  padding-top: 1.5rem;
  text-align: right;
  margin: 0.2rem;
  font-size: 1rem;
  outline: none;
}

.buff {
  position: absolute;
  top: 0.6rem;
  right: 0.7rem;
  font-size: 0.8rem;
}

.row {
  display: table-row;
}

.cell {
  display: table-cell;
}

.btn {
  width: 5rem;
  height: 2rem;
  margin: 0.2rem;
  font-size: 1.3rem;
}

</style>
