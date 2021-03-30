<template>
  <div>
    <img id="yeezy" alt="kanye mad" src="https://i.pinimg.com/originals/b6/43/13/b64313085b888070afafe4c55c22106c.jpg">
    <h1>What is Kanye West thinking about?</h1>
    <h3>{{quote}}</h3>
    <button id="moreYeezy" v-on:click="moreYeezy">More Kanyeisms</button>
  </div>
</template>

<script>
export default {
  name: "KanyeRest",
  data() {
    return {
      quote: ''
    };
  },
  // On page load, GET a Kanye tweet
  async created() {
    // Simple GET request using fetch
    const response = await fetch("https://api.kanye.rest");
    const data = await response.json();
    this.quote = data.quote;
  },
  methods: {
    // GET new quote on button click, with Error handling
    async moreYeezy() {
      fetch("https://api.kanye.rest")
        .then(async response => {
          const data = await response.json();

          if (!response.ok) {
            const error = (data && data.message) || response.statusText;
            return Promise.reject(error);
          }

          this.quote = data.quote;
          let kanyeImage = document.getElementById("yeezy");

          const images = [
            "https://i.pinimg.com/originals/b6/43/13/b64313085b888070afafe4c55c22106c.jpg",
            "https://storage.googleapis.com/afs-prod/media/1f764b198a42470189b99b4084be6cf0/800.jpeg",
            "https://static.billboard.com/files/media/kanye-west-whh-2018-billboard-1548-compressed.jpg",
            "https://quincy-network.s3.ca-central-1.amazonaws.com/wp-content/uploads/sites/8/2020/08/0803_kanye-860x645.jpg",
            "https://variety.com/wp-content/uploads/2020/07/kanye-west-1-e1599269208476.jpg",
            "https://media.vanityfair.com/photos/56c4bdf3dc63709f7857b062/16:9/w_1280,c_limit/kanye-west-really-in-debt.jpg",
            "https://static.highsnobiety.com/thumbor/-blbXfjnMdxygFK8_gbpGK_-PB0=/1600x1067/static.highsnobiety.com/wp-content/uploads/2020/10/28185230/kanye-west-building-city-haiti-01.jpg",
            "https://cdn.vox-cdn.com/uploads/chorus_asset/file/20019490/kanye_west_GC_IMAGES.jpg",
            "https://dazedimg-dazedgroup.netdna-ssl.com/640/0-0-1080-720/azure/dazed-prod/1280/1/1281206.jpg"
          ];

          let image = images[Math.floor(Math.random() * images.length)]

          kanyeImage.src = image;
        })
        .catch(error => {
          this.errorMessage = error;
          console.error("Somthin dun broke: ", error);
        });
    }
  }
};
</script>

<style scoped>
  img {
    border-radius: 50%;
    max-height: 300px;
  }

  h3 {
    color: #3f3f3f;
  }

  button {
    padding: 1em;
    font-size: 1em;
    color: #ffffff;
    background-color: #6f9ac9;
    border: 1px solid #2c3e50;
    border-radius: 5%;
    margin-bottom: 5em;
    transition:all 100ms;
  }

  button:hover {
    color: #e9e9e9;
    background-color: #2c3e50;
    border: 1px solid #6f9ac9;
  }
</style>