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
import calc from '@/lib/calculate'

export default {
  data () {
    return {
      buttons: [
        [
          {
            title: '(',
            type: 'operator',
            value: '('
          },
          {
            title: ')',
            type: 'operator',
            value: ')'
          },
          {
            title: '%',
            type: 'operator',
            value: ''
          },
          {
            title: 'CE',
            type: 'cancel',
            value: ''
          }
        ],
        [
          {
            title: '7',
            type: 'number',
            value: '7'
          },
          {
            title: '8',
            type: 'number',
            value: '8'
          },
          {
            title: '9',
            type: 'number',
            value: '9'
          },
          {
            title: '&divide;',
            type: 'operator',
            value: '/'
          }
        ],
        [
          {
            title: '4',
            type: 'number',
            value: '4'
          },
          {
            title: '5',
            type: 'number',
            value: '5'
          },
          {
            title: '6',
            type: 'number',
            value: '6'
          },
          {
            title: '&times;',
            type: 'operator',
            value: '*'
          }
        ],
        [
          {
            title: '1',
            type: 'number',
            value: '1'
          },
          {
            title: '2',
            type: 'number',
            value: '2'
          },
          {
            title: '3',
            type: 'number',
            value: '3'
          },
          {
            title: '-',
            type: 'operator',
            value: '-'
          }
        ],
        [
          {
            title: '0',
            type: 'number',
            value: '0'
          },
          {
            title: '.',
            type: 'operator',
            value: '.'
          },
          {
            title: '=',
            type: 'enter',
            value: ''
          },
          {
            title: '+',
            type: 'operator',
            value: '+'
          }
        ]
      ],
      value: ''
    }
  },
  methods: {
    inputBtn (btn) {
      /* eslint-disable */
      if (btn.type === 'number' || 'operator') this.value += btn.value
      if (btn.type === 'cancel') this.value = ''
      if (btn.type === 'enter') this.value = calc(this.value)
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
