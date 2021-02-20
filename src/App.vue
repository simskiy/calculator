<template lang="pug">
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
.calc {
  margin: auto;
}
</style>
