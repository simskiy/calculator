<template lang="pug">
  div.calculator
    input.input(type="text")
    span.buff hello
    div.wrapper
      div.row(v-for="row in buttons")
        div.cell(v-for="cell in row")
          button.btn(v-html="cell.value")
</template>

<script>
export default {
  data () {
    return {
      buttons: [
        [{ value: '(', type: 'operator' }, { value: ')', type: 'operator' }, { value: '%', type: 'operator' }, { value: 'CE', type: 'operator' }],
        [{ value: '7', type: 'number' }, { value: '8', type: 'number' }, { value: '9', type: 'number' }, { value: '&divide;', type: 'operator' }],
        [{ value: '4', type: 'number' }, { value: '5', type: 'number' }, { value: '6', type: 'number' }, { value: '&times;', type: 'operator' }],
        [{ value: '1', type: 'number' }, { value: '2', type: 'number' }, { value: '3', type: 'number' }, { value: '-', type: 'operator' }],
        [{ value: '0', type: 'number' }, { value: '.', type: 'operator' }, { value: '=', type: 'operator' }, { value: '+', type: 'operator' }]
      ]
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
