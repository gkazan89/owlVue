<template>
  <div class="home">
    <h1>Articles</h1>
    <div v-for="art in articles">
    <p>{{art[artDex].sectionName}}</p>
    <h2>{{art[artDex].webTitle}}</h2>
    <p>{{art[artDex]}}</p>
    <p>{{artDex}}</p>
    <button v-on:click="artDex += 1">Plus button</button>
    <button v-on:click="artDex -= 1">Minus button</button>
    </div>
  </div>
</template>

<style>
.article_img img {
  display: block;
  max-width: 500px;
  max-height: 300px;
}
</style>

<script>
var axios = require("axios");
export default {
  data: function() {
    return {
      articles: [],
      artDex: 0,
      num: 0
    };

  },
  // make request to articles view to retrieve first and second item in category JSON data
  created: function() {
    axios.get("http://localhost:3000/api/view").then(
      function(response) {
        console.log("ARTICLES");
        console.log(response);
        this.articles = response.data;
      }.bind(this)
    );
    console.log(this);

    // var other = axios.get();
  },

  methods: {},
  computed: {}
};
</script>
