<template>
  <div id="app">
    <HomePage msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HomePage from './components/HomePage.vue'

export default {
  name: 'App',
  components: {
    HomePage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #2c3e50;
  color: aliceblue;
  /* color: #2c3e50; */
  margin-top: 60px;
}
*{outline: 2px red solid;}
html {
  background-color: #2c3e50;
}
</style>
