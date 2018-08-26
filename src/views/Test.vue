<template>
  <div class="home">
    <h1>Articles</h1>
    <div>
      <div v-for="category in categories">
        <h2>{{category.category}}</h2>
        <h4>{{ category.data[category.currentArticleIndex].webTitle }}</h4>
        <button v-on:click="upOne(category)">Up One</button>
        <button v-on:click="downOne(category)">Down One</button>
        <p>{{category.currentArticleIndex}}</p>
      </div>  
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
      categories: [],
      // can't affect all other categories....
    };

  },
  // make request to categories view to retrieve first and second item in category JSON data
  created: function() {
    axios.get("http://localhost:3000/api/test").then(
      function(response) {
        console.log("categories");
        console.log(response);
        this.categories = response.data;
      }.bind(this)
    );
    console.log(this);

    // var other = axios.get();
  },

  methods: {
    upOne: function(category) {
      if (category.currentArticleIndex < category.data.length) {
        category.currentArticleIndex += 1;
      }
      console.log(category.currentArticleIndex);
    },
    downOne: function(category) {
      if (category.currentArticleIndex > 0) {
        category.currentArticleIndex -= 1;
      }
      console.log(category.currentArticleIndex);
    }
  },
  computed: {}
};
</script>
