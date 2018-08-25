<template>
  <div class="home">
    <h2>Articles</h2>
    <div v-for="art in articles">
<!--       <div class="article_img">
        <h2>{{  art.title  }}</h2>
        <h3>{{  art.author  }}</h3> -->
        <!-- <img v-bind:src="art.master_image" alt = "">
        <p v-html="art.body"></p> -->
      <p>First link:</p>
      <p>{{  art.READ_THIS_apiUrl  }}</p>
      <button>Press button</button>
      <p>Next link:</p>
      <p>{{  art.next_api_up  }}</p>
      
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
      articles: []
    };
  },
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
