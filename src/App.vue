<template>
  <div class="home">
    <p>Weather in...</p>
    <WeatherCard />
  </div>
</template>

<script>
import WeatherCard from './components/WeatherCard.vue'

export default {
  name: 'App',
  components: {
    WeatherCard
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
p {
  font-weight: bold;
  font-size: 20px;
  margin: auto;
}
</style>
