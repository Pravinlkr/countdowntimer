<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <timer></timer>
  <control></control>
</template>

<script>
import Timer from './components/Timer.vue'
import Control from './components/Control.vue'

export default {
  name: 'App',
  components: {
    Timer,
    Control
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
  margin-top: 30px;
}
img{
  height: 150px;
}
</style>
