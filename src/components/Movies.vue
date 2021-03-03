<template>
  <div>
    <h1>Movies, TV &amp; More</h1>
    <p>Search a movie, TV show or video game title to get started.</p>
    <input
      v-model="movieTitle"
      v-on:keyup="movieSearch(movieTitle)"
      v-on:blur="movieSearch(movieTitle)"
      placeholder="Enter a Title" />

    <button v-if="pageNumber > 1" v-on:click="prevPage(pageNumber-=1, movieTitle)">Previous Page</button>
    <button v-if="data.totalResults > 10" v-on:click="nextPage(pageNumber+=1, movieTitle)">Next Page</button>

    <h3 v-if="data.totalResults">Total results for {{ movieTitle }}: {{ data.totalResults }}</h3>

    <div id="movies">
      <div class="movie" v-for="(movie, index) in data.Search" :key="index">
        <a v-bind:href="'http://www.imdb.com/title/'+  movie.imdbID" target="_blank">
          <img v-if="movie.Poster !== 'N/A'" v-bind:src="movie.Poster" v-bind:alt="movie.Title">
          <img v-if="movie.Poster === 'N/A'" src="https://via.placeholder.com/300x425?text=No+Image+Found" v-bind:alt="movie.Title">
        </a>
          <div class="movieTitleYear">
            <h2>{{ movie.Title }}</h2>
            <span>{{ movie.Type }}</span>
            <span> ({{ movie.Year }})</span>
          </div>
      </div>
    </div>

    <button v-if="pageNumber > 1" v-on:click="prevPage(pageNumber-=1, movieTitle)">Previous Page</button>
    <button v-if="data.totalResults > 10" v-on:click="nextPage(pageNumber+=1, movieTitle)">Next Page</button>

  </div>
</template>

<script>
export default {
  name: 'Get Movies',
  data() {
    return {
      data: {},
      movieTitle: '',
      imdbID: '',
      totalResults: 0,
      pageNumber: 1
    };
  },
  async created() {

  },
  methods: {
    async movieSearch(movieTitle) {
      // You will need to go to https://rapidapi.com/rapidapi/api/movie-database-imdb-alternative
      // and register for an API key to get this movie example to work correctly.
      // Simply replace [process.env.VUE_APP_API_KEY] wtih your API key below, or register it in a local .env file
      const apiKey = process.env.VUE_APP_API_KEY;
      const apiHost = "movie-database-imdb-alternative.p.rapidapi.com";
      const apiUrl = "https://movie-database-imdb-alternative.p.rapidapi.com/?r=json&page=1&s=" + movieTitle;

      fetch(apiUrl, {
        "method": "GET",
        "headers": {
          "x-rapidapi-key": apiKey,
          "x-rapidapi-host": apiHost
        }
      })
      .then(async response => {
        const data = await response.json();
        console.log(data);
        this.data = data;
      })
      .catch(error => {
        this.errorMessage = error;
        console.log("Ya'll done said no response", error)
      });
    },
    async nextPage(pageNumber, movieTitle){
      const apiKey = process.env.VUE_APP_API_KEY;
      const apiHost = "movie-database-imdb-alternative.p.rapidapi.com";
      const movieApiUrl = "https://movie-database-imdb-alternative.p.rapidapi.com/?" + "s=" + movieTitle + "&r=json&page=" + pageNumber;

      fetch(movieApiUrl, {
        "method": "GET",
        "headers": {
          "x-rapidapi-key": apiKey,
          "x-rapidapi-host": apiHost
        }
      })
      .then(async response => {
        const data = await response.json();
        console.log(data);
        this.data = data;
      })
      .catch(error => {
        this.errorMessage = error;
        console.log("Ya'll done said no response", error)
      });
    },

    async prevPage(pageNumber, movieTitle){
      const apiKey = process.env.VUE_APP_API_KEY;
      const apiHost = "movie-database-imdb-alternative.p.rapidapi.com";
      const movieApiUrl = "https://movie-database-imdb-alternative.p.rapidapi.com/?" + "s=" + movieTitle + "&r=json&page=" + pageNumber;

      fetch(movieApiUrl, {
        "method": "GET",
        "headers": {
          "x-rapidapi-key": apiKey,
          "x-rapidapi-host": apiHost
        }
      })
      .then(async response => {
        const data = await response.json();
        console.log(data);
        this.data = data;
      })
      .catch(error => {
        this.errorMessage = error;
        console.log("Ya'll done said no response", error)
      });

    }
  }
}
</script>