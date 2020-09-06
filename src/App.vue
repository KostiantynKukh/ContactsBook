<template>
  <div id="app">    
    <home />
  </div>
</template>

<script>
import Home from '@/views/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style lang="scss">
*, *::before, *::after {
  margin: 0;
  padding: 0;
  border: 0; 
  vertical-align: baseline;
  box-sizing: border-box;  
}
html {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 10px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  background: rgb(185, 216, 210);
}
</style>
