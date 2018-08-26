<template>
  <div class="home">
    <h1>Articles</h1>
    <div>
      <div v-for="category in categories">
        <h2>{{category.category}}</h2>
        <h4>{{ category.data[category.currentArticleIndex].webTitle }}</h4>
        <p>{{category.data[category.currentArticleIndex].apiUrl}}</p>
        <div>
          <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored" v-on:click="upOne(category)">Up One</button>
        </div>
        <div>
          <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--accent" v-on:click="downOne(category)">Down One</button>
        </div>
        <div>
          <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored" id="show-dialog" v-on:click="read(category)">READ</button>
        </div>
        <div>
          <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--accent" v-on:click="visible(category)">VISIBLE</button>
        </div>
<!--         <p v-html="info.response.content.blocks.body[0].bodyHtml"></p> -->
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
      info: []
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
      // console.log(category.currentArticleIndex);
    },
    downOne: function(category) {
      if (category.currentArticleIndex > 0) {
        category.currentArticleIndex -= 1;
      }
      // console.log(category.currentArticleIndex);
    },
    read: function(category) {
      console.log(category.currentArticleIndex);
      var link = category.data[category.currentArticleIndex].apiUrl;
      var key = process.env.VUE_APP_MY_API_KEY;
      var test = axios.get(link + "?show-blocks=all&api-key=" + key).then(
        function(response) {
          this.info = response.data;
        }.bind(this)
      );
      console.log(this);
    },

    visible: function(category) {
      console.log(category.currentArticleVisible);
    }
  },
  computed: {}
};
</script>
