<template lang="html">
  <div class="weather-display">
  <p>IMG OF WEATHER TYPE</p>
  <p>{{weatherForecast.main.temp}}°C</p>
  <p>{{weatherForecast.weather[0].description}}</p>
  <!-- <p>Real Feel: {{weatherForecast.main.feels_like}}°C</p>
  <p>Humidity: {{weatherForecast.main.humidity}}%</p> -->
</div>
</template>

<script>
export default {
  name: "display-weather",
  props: ['weatherForecast']
}
</script>

<style lang="css" scoped>

.weather-display {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;

  min-width: 300px;
}
</style>
