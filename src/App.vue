<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <Weather/>
  </div>
</template>

<script>
import Weather from './components/Weather.vue'

export default {
  name: 'App',
  components: {
    Weather
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  
}

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
