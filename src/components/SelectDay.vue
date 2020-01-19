<template lang="html">
  <div>
    <h4>Five day forecast:</h4>
    <select v-model="selectedDate" @change='selectDate'>
      <option v-for='(weatherArray, date) in fiveDayForecast'>{{date}}</option>
    </select>
  </div>
</template>

<script>
import { eventBus } from '../main.js';
const moment = require('moment');

// console.log(moment().add(1, 'day').add(3, 'hours').format('YYYY-MM-DD 18:00:00'));

export default {
  name: "select-day",
  data(){
    return {
      selectedDate: []
    }
  },
  props: ['fiveDayForecast'],
  methods: {
    selectDate(){
      eventBus.$emit('send-selected-date-info', this.selectedDate);
    }
  }
}
</script>

<style lang="css" scoped>

select {
  background-color: #E0FBFC;
}
</style>
