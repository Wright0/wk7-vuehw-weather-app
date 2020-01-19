<template>
  <div id="app">
    <h1>Edinburgh Weather</h1>
    <select-day :upcomingWeather='upcomingEDIWeather'/>
    <display-weather :currentWeather='currentEDIWeather' :weatherForecast='selectedWeatherObject'/>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import SelectDay from './components/SelectDay.vue'
import DisplayWeather from './components/DisplayWeather.vue'

export default {
  name: 'app',
  data(){
    return {
      currentEDIWeather: {},
      upcomingEDIWeather: [],
      selectedWeatherObject: null
    }
  },
  components: {
    "select-day": SelectDay,
    "display-weather": DisplayWeather
  },
  mounted(){
    fetch('https://api.openweathermap.org/data/2.5/weather?id=3333229&units=metric&APPID=845746c8172a51a966b8c21712af5d3f')
    .then(response => response.json())
    .then(currentEDIWeatherDetails => this.currentEDIWeather = currentEDIWeatherDetails)

    fetch('https://api.openweathermap.org/data/2.5/forecast?id=3333229&units=metric&APPID=845746c8172a51a966b8c21712af5d3f')
    .then(response => response.json())
    .then(upcomingEDIWeatherObject => this.upcomingEDIWeather = upcomingEDIWeatherObject.list)

    eventBus.$on('send-dt-selected', dateTimeCode => {
      this.selectedWeatherObject = this.upcomingEDIWeather.find(weatherObject => weatherObject.dt === dateTimeCode)
    })

    console.log(combineFiveDaysData());
  },
  methods: {
    combineFiveDaysData(){
        const numberTest = [1, 2, 3, 4, 5]
        let fiveDays = {};

        numberTest.map(number => {
          fiveDays[number] = 'test123';
        })

        return fiveDays
      }


  }

}
</script>

<style>
body {
  background-color: #2F2235;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #BFC3BA;
  margin-top: 60px;
}
</style>
