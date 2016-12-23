<template>
  <div id="app">
    <img src="./assets/logo.png">
    <vesta></vesta>
  </div>
</template>

<script>
import Vesta from './components/Vesta'

export default {
  name: 'app',
  components: {
    Vesta
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
