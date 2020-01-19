<template>
  <div id="app">
    <h1>Hello</h1>
    <select-day />
    <display-weather />
  </div>
</template>

<script>
import SelectDay from './components/SelectDay.vue'
import DisplayWeather from './components/DisplayWeather.vue'

export default {
  name: 'app',
  components: {
    "select-day": SelectDay,
    "display-weather": DisplayWeather
  },

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
