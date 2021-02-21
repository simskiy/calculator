<template lang="pug">
div.wrapper
  calculator.calc
</template>

<script>
import calculator from '@/components/calculator.vue'
export default {
  name: 'App',
  components: {
    calculator
  }
}
</script>

<style lang="scss">
.wrapper {
  display: flex;
  width: 100%;
}
.calc {
  margin: auto;
}
</style>
