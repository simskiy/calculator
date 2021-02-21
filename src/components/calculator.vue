<template lang="pug">
  div.calculator(ref="calc")
    input.input(
      type="text"
      v-model="value"
      @keyup="pressKey($event)"
      ref="input"
      autofocus
    )
    span.buff {{prevResult}}
    div.wrapper
      transition(name="slide-fade")
        div.table.table--left(v-if="show")
          div.row(v-for="row in extButtons")
            div.cell(v-for="cell in row")
              button.btn(
                v-html="cell.title"
                @click="pressBtn(cell)"
            )
      div.table.table--right
        div.row(v-for="row in buttons")
          div.cell(v-for="cell in row")
            button.btn(
              v-html="cell.title"
              @click="pressBtn(cell, $event)"
          )
</template>

<script>
import btns from './btns.js'
import extBtns from './extBtns.js'
import { create, all } from 'mathjs'

export default {
  data () {
    return {
      buttons: btns,
      extButtons: extBtns,
      value: '',
      prevResult: '',
      show: false
    }
  },
  methods: {
    pressBtn (btn, event) {
      this.$refs.input.focus()
      switch (btn.type) {
        case ('number'):
        case ('operator'): this.value += btn.value
          break
        case ('cancel'): this.value = ''
          break
        case ('enter'): this.value = this.result(this.value)
          break
        case ('showExt'): {
          this.show = !this.show
          setTimeout(() => {
            event.target.innerText = this.show ? '=>' : '<='
          }, 300)
        }
      }
    },
    pressKey (event) {
      switch (event.keyCode) {
        case (13): this.value = this.result(this.value)
      }
    },
    result (value) {
      const math = create(all)
      const limitedEvaluate = math.evaluate

      math.import({
        import: 'Function import is disabled',
        createUnit: 'Function createUnit is disabled',
        evaluate: 'Function evaluate is disabled',
        parse: 'Function parse is disabled',
        simplify: 'Function simplify is disabled',
        derivative: 'Function derivative is disabled'
      }, { override: true })

      this.prevResult = value
      return limitedEvaluate(value)
    }
  }
}
</script>

<style lang="scss" scoped>
$transition-time: 0.3s;

.slide-fade-enter-active {
  transition: all $transition-time cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-leave-active {
  transition: all $transition-time cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active до версии 2.1.8 */ {
  transform: translateX(1rem);
  opacity: 0;
}

html {
  font-size: 16px;
}

.calculator {
  position: relative;
  border: 1px solid black;
  border-radius: 5px;
  padding: 0.3rem;
}

.table {
  display: inline-block;
  &--left {
    margin-right: 1rem;
  }
  &--right {
    margin-left: auto;
  }
}

.input {
  box-sizing: border-box;
  width: calc(100% - 0.4rem);
  padding: 0.3rem;
  padding-top: 1.5rem;
  text-align: right;
  margin: 0.2rem;
  font-size: 1rem;
  outline: none;
}

.buff {
  position: absolute;
  top: 0.6rem;
  right: 0.9rem;
  font-size: 0.8rem;
  color: grey;
  opacity: 0.8;
}

.row {
  display: flex;
  align-items: center;
}

.btn {
  width: 4rem;
  height: 2rem;
  margin: 0.2rem;
  padding: 0;
  font-size: 1.1rem;
  outline: none;
}

</style>
