<template lang="html">
  <div>
    <div class="weather-display" v-if="!weatherForecast">
      <h3>Current Weather</h3>
      <img :src="iconLinkCurrent" alt="Weather icon">
      <p>{{currentWeather.main.temp}}°C</p>
      <p>{{currentWeather.weather[0].description}}</p>
    </div>

    <div class="weather-display" v-if="weatherForecast">
      <img :src="iconLinkFuture" alt="Weather icon">
      <p>{{weatherForecast.main.temp}}°C</p>
      <p>{{weatherForecast.weather[0].description}}</p>
      <p>Real Feel: {{weatherForecast.main.feels_like}}°C</p>
      <p>Humidity: {{weatherForecast.main.humidity}}%</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "display-weather",
  props: ['weatherForecast', 'currentWeather'],
  computed:{
    iconLinkFuture(){
      return `http://openweathermap.org/img/wn/${this.weatherForecast.weather[0].icon}@2x.png`
    },
    iconLinkCurrent(){
      return `http://openweathermap.org/img/wn/${this.currentWeather.weather[0].icon}@2x.png`
    }
  }

}
</script>

<style lang="css" scoped>

.weather-display {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  min-width: 250px;
  /* max-width: 500px; */
  border: 1px solid #BFC3BA;

  margin: 15px;
}
</style>
