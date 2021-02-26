<template>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <Kanyeisms /> -->
  <Movies />
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
//import Kanyeisms from './components/Kanyeisms.vue'
import Movies from './components/Movies.vue'

export default {
  name: 'App',
  components: {
    //HelloWorld,
    //Kanyeisms
    Movies
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
  margin: 4em 2em;
}
</style>
