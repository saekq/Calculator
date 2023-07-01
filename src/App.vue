<template>
  <div id="app">
    <calc></calc>
  </div>
</template>

<script>
import calc from './components/calc.vue'

export default {
  name: 'App',
  components: {
    calc
  }
}
</script>

<style>
  * {
    background: #313131;
  }
</style>
