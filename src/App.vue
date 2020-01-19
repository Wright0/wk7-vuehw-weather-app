<template>
  <div id="app">
    <h1>Edinburgh Weather</h1>
    <display-current-weather :currentWeather='currentWeather'/>
    <select-day :fiveDayForecast='fiveDayForecast'/>
    <display-forecast :selectedDayArray='selectedDayArray'/>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import SelectDay from './components/SelectDay.vue'
import DisplayForecast from './components/DisplayForecast.vue'
import DisplayCurrentWeather from './components/DisplayCurrentWeather.vue'

export default {
  name: 'app',
  data(){
    return {
      currentWeather: null,
      fiveDayForecast: {},
      selectedDayArray: null,
    }
  },
  components: {
    "select-day": SelectDay,
    "display-forecast": DisplayForecast,
    "display-current-weather": DisplayCurrentWeather
  },
  mounted(){
    fetch('https://api.openweathermap.org/data/2.5/weather?id=3333229&units=metric&APPID=845746c8172a51a966b8c21712af5d3f')
    .then(response => response.json())
    .then(currentWeatherDetails => this.currentWeather = currentWeatherDetails)

    fetch('https://api.openweathermap.org/data/2.5/forecast?id=3333229&units=metric&APPID=845746c8172a51a966b8c21712af5d3f')
    .then(response => response.json())
    .then(nextFiveDaysObject => {
      //Get the unique dates.
      let allDates = nextFiveDaysObject.list.map(weatherObject => weatherObject.dt_txt.substring(0, 10));
      const uniqueDates = new Set(allDates);

      //Build the data structure. Combine all objects from the same day together in one array set to a key of that date.
      uniqueDates.forEach(date => {
        this.fiveDayForecast[date] = nextFiveDaysObject.list.filter(weatherObject => {
          return weatherObject.dt_txt.substring(0,10) === date
        })
      });
    })

    eventBus.$on('send-selected-date-info', selectedDayWeatherArray => {
      selectedDayArray = selectedDayWeatherArray
    })
  }
}
</script>

<style>
body {
  background-color: #253237;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #E0FBFC;
  margin-top: 60px;
}
</style>
