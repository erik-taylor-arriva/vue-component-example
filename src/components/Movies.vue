<template>
  <div>
    <img v-bind:src="data.Poster" alt="movie poster">
    <h2>{{ data.Title }}</h2>
    <p>{{ data.Plot }}</p>
    <p><strong>Ratings:</strong></p>
    <ul>
      <li v-for="rating in data.Ratings" v-bind:key="rating.Value">
        {{ rating.Source }} {{ rating.Value }}
      </li>
    </ul>

    <div id="loopParams">
      <p><strong>Loop through all params:</strong></p>
      <p v-for="(value, name, index) in data" :key="index">
        <strong>{{ name }}:</strong> {{ value }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'get-request',
  data() {
    return {
      data: {}
    };
  },
  async created() {
    // You will need to go to https://rapidapi.com/rapidapi/api/movie-database-imdb-alternative
    // and register for an API key to get this movie example to work correctly.
    // Simply replace [process.env.VUE_APP_API_KEY] wtih your API key below, or register it in a local .env file
    let apiKey = process.env.VUE_APP_API_KEY;

    fetch("https://movie-database-imdb-alternative.p.rapidapi.com/?i=tt0047034&r=json", {
      "method": "GET",
      "headers": {
        "x-rapidapi-key": apiKey,
        "x-rapidapi-host": "movie-database-imdb-alternative.p.rapidapi.com"
      }
    })
    .then(async response => {
      const data = await response.json();
      console.log(data);
      this.data = data;
    })
    .catch(err => {
      console.error(err);
    });
  }
}
</script>

<style scoped>
  p, ul {
    text-align: left;
  }
</style>