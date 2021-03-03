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
body {
  background-image: url('./assets/curtains.png');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: top;
  background-attachment: fixed;
  max-width: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 10em 1em 4em;
  font-size: 1.2em;
}

#movies {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  max-width: 1200px;
  margin: 0 auto;
}

.movie {
  animation: diplay-movie 5s ease 0.2s;
}

@keyframes display-movie {
    0% {
        opacity: 0;
        transform: scale(0.5,0.5);
    }
    100% {
        opacity: 1;
        transform: scale(1,1);
    }
}

p, ul {
  text-align: center;
}

.movieTitleYear {
  margin: 1em;
  max-width: 315px;
}

h1 {
  margin-bottom: 0;
}

h2 {
  font-size: 1em;
  margin: 0;
}

img {
  margin: 1em 1em 0em;
  max-height: 425px;
}

button {
  margin: 1em;
}

input {
  display: block;
  margin: 0 auto;
  padding: 0.5em;
  text-align: center;
  font-size: 1em;
  text-transform: capitalize;
}
</style>
