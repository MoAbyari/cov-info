<template>
  <div class="container">
    <div>
      <h2>Lives lost by age group</h2>
      <bar-chart v-if="loaded" :chartData="chartData"></bar-chart>
    </div>
  </div>
</template>

<script>
import BarChart from './BarChart.vue';
import { api } from '../helpers/helpers';

export default {
  name: 'DeathsBarChart',
  components: { BarChart },
  data: () => ({
    loaded: false,
    chartData: null
  }),
  async mounted () {
    this.loaded = false
    try {
      const data = await api.getDeathsByAge();
      this.chartData = data
      this.loaded = true
    } catch (e) {
      console.error(e)
    }
  }
}
</script>

<style scoped>
.container {
  background-color: #0058A9;
  padding: 30px 29px 60px 29px;
}

.container div {
  background-color: white;
  padding: 20px 5px;
  border-radius: 15px;
}

.container h2 {
  font-size: 21px;
  text-align: center;
  margin-top: 25px;
}
</style>

