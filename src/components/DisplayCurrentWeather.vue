<template lang="html">
  <div class="weather-display" v-if="currentWeather">
    <h2>Current Weather</h2>
    <div class="weather-info">
      <img :src="iconLink" alt="Weather icon">
      <p>{{currentWeather.main.temp.toFixed()}}°C</p>
      <p>{{currentWeather.weather[0].description}}</p>
      <p>Humidity: {{currentWeather.main.humidity}}%</p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'display-current-weather',
  props: ['currentWeather'],
  computed:{
    iconLink(){
      return `http://openweathermap.org/img/wn/${this.currentWeather.weather[0].icon}@2x.png`
    }
  }
}
</script>

<style lang="css" scoped>

p {
  font-size: 20px;
  margin: 0px;
}

.weather-display {
  display: flex;
  flex-direction: column;
  min-width: 250px;
  max-width: 500px;
  border: 1px solid #BFC3BA;
  border-radius: 5px;
  margin: 15px auto;
}

.weather-info {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;
  margin: 0px;
}
</style>
