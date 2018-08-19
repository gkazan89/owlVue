<template>
  <div class="home">
    <h2>Articles</h2>
    <div v-for="art in articles">
      <h2>{{  art.title  }}</h2>
      <h3>{{  art.author  }}</h3>
      <p v-html="art.body"></p>
    </div>

  </div>
</template>

<style>
</style>

<script>
var axios = require("axios");
export default {
  data: function() {
    return {
      preferences: [],
      articles: []
    };
  },
  created: function() {
    axios.get("http://localhost:3000/api/preferences").then(
      function(response) {
        console.log(response);
        this.preferences = response.data;
      }.bind(this)
    );

    axios.get("http://localhost:3000/api/articles").then(
      function(response) {
        console.log(response);
        this.articles = response.data;
      }.bind(this)
    );
  },

  methods: {},
  computed: {}
};
</script>
