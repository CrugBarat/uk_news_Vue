<template lang="html">
  <GChart
  :type="chartType"
  :data="chartData"
  :options="chartOptions"
  />
</template>

<script>
import {eventBus} from '../main.js'
import {GChart} from 'vue-google-charts'

export default {
  name: 'covid-chart',
  props: ['covidData'],
  data(){
    return {
      chartOptions: {
        height: 450,
        colors: ['#034078'],
        backgroundColor: '#edf2f4',
      },
      chartType: "ColumnChart"
    }
  },
  components : {
    GChart
  },
  computed: {
    chartData () {
      if (this.covidData) {
        const chartData = this.covidData.map(cases => Object.values(cases));
        chartData[0] = Object.keys(this.covidData[0]);
        return chartData;
      }
      return null;
    }
  }
}
</script>

<style lang="css" scoped>
</style>
