<template>
  <div>
    <h1>Godzilla Showcase</h1>
    <button v-if="pageNumber > 1" v-on:click="nextPage(pageNumber-=1)">Previous Page</button>
    <button v-on:click="nextPage(pageNumber+=1)">Next Page</button>
    <div id="movies">
      <div class="movie" v-for="(movie, index) in data.Search" :key="index">
          <img v-if="movie.Poster !== 'N/A'" v-bind:src="movie.Poster" v-bind:alt="movie.Title">
          <img v-if="movie.Poster === 'N/A'" src="https://via.placeholder.com/300x425?text=No+Image+Found" v-bind:alt="movie.Title">
          <div class="movieTitleYear">
            <h2>{{ movie.Title }}</h2>
            <span>{{ movie.Type }}</span>
            <span> ({{ movie.Year }})</span>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'get-request',
  data() {
    return {
      data: {},
      //movieName: '', TODO bind movie title to a search input
      pageNumber: 1
    };
  },
  async created() {
    // You will need to go to https://rapidapi.com/rapidapi/api/movie-database-imdb-alternative
    // and register for an API key to get this movie example to work correctly.
    // Simply replace [process.env.VUE_APP_API_KEY] wtih your API key below, or register it in a local .env file
    const apiKey = process.env.VUE_APP_API_KEY;
    const apiHost = "movie-database-imdb-alternative.p.rapidapi.com";

    // A list of Godzilla movies
    const godzillasApiUrl = "https://movie-database-imdb-alternative.p.rapidapi.com/?s=Godzilla&r=json";

    fetch(godzillasApiUrl, {
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
    .catch(err => {
      console.error(err);
    });
  },
  methods: {
    // TODO: write movie title search
    // async movieSearch(movieTitle) {

    // },
    async nextPage(pageNumber){
      const apiKey = process.env.VUE_APP_API_KEY;
      const apiHost = "movie-database-imdb-alternative.p.rapidapi.com";
      const godzillasApiUrl = "https://movie-database-imdb-alternative.p.rapidapi.com/?s=Godzilla&r=json&page=" + pageNumber;

      fetch(godzillasApiUrl, {
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

    async prevPage(pageNumber){
      const apiKey = process.env.VUE_APP_API_KEY;
      const apiHost = "movie-database-imdb-alternative.p.rapidapi.com";
      const godzillasApiUrl = "https://movie-database-imdb-alternative.p.rapidapi.com/?s=Godzilla&r=json&page=" + pageNumber;

      fetch(godzillasApiUrl, {
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

<style scoped>
  #movies {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    max-width: 1200px;
    margin: 0 auto;
  }

  p, ul {
    text-align: center;
  }

  .movieTitleYear {
    margin-bottom: 1em;
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
</style>