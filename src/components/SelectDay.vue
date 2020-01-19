<template lang="html">
  <div>
    <select v-model="dtOfdateSelected" @change='selectDate'>
      <option v-for='weatherObjects in upcomingWeather' :value='weatherObjects.dt'>{{weatherObjects.dt_txt}}</option>
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
      dtOfdateSelected: ''
    }
  },
  props: ['upcomingWeather'],
  methods: {
    selectDate(){
      eventBus.$emit('send-dt-selected', this.dtOfdateSelected);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
