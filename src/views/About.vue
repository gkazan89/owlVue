<template>
  <div class="about">
    <h1>Articles:</h1>
    
    <div v-for="art in articles">
      <h2>{{  art.title  }}</h2>
      <h2>{{  art.category  }}</h2>
      <p>{{  art.author  }}</p>
      <p>{{  art.body  }}</p>
    </div>

  </div>
</template>




<script>
var axios = require("axios");
export default {
  data: function() {
    return {
      articles: []
    };
  },
  readArticles: function(readArticles) {
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
