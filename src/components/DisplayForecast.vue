<template lang="html">
  <div class="weather-display" v-if="selectedDayArray">
    <img :src="iconLink" alt="Weather icon">
    <p>{{selectedDayArray.main.temp.toFixed()}}°C</p>
    <p>{{selectedDayArray.weather[0].description}}</p>
    <p>Real Feel: {{selectedDayArray.main.feels_like.toFixed()}}°C</p>
    <p>Humidity: {{selectedDayArray.main.humidity}}%</p>
  </div>
</template>

<script>
export default {
  name: "display-forecast",
  props: ['selectedDayArray'],
  computed:{
    iconLink(){
      return `http://openweathermap.org/img/wn/${this.selectedDayArray.weather[0].icon}@2x.png`
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
