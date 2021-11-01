<template>
  <div id="app">
    <Canculator />
  </div>
</template>

<script>
import Canculator from './components/Canculator.vue'

export default {
  name: 'App',
  components: {
    Canculator
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
