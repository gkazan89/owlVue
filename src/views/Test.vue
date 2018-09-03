<template>
  <div class="home">
    <h1>Articles</h1>
    <div class="list">
      <div class="reading" v-for="category in categories">
        <h2>{{category.category}} News</h2>
        <h4>{{category.data[category.currentArticleIndex].webTitle}}</h4>
        <!-- <img v-bind:src="info.response.content.blocks.elements[0].assets[0].file"> WANT IMAGE!!! --> 
        <div class="buttonNavs">
          <div class="kids">
            <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored" v-on:click="downOne(category)">Back</button>
          </div>
          <div class="kids">
            <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--accent" id="show-dialog" v-on:click="read(category)">READ ARTICLE</button>
          </div>
          <div class="kids">
            <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored" v-on:click="upOne(category)">Next</button>
          </div>
        </div>  
        <p class="reading" v-if="category.currentArticleVisible" v-html="info.response.content.blocks.body[0].bodyHtml"></p>
      </div>  
    </div>
  </div>
</template>

<style>

  h2 {
    text-transform: uppercase;
  }

  .list, .reading {
    border: 2px solid black;
  }

  .reading img{
    max-height: 300px;
    max-width: 500px;
  }

  .buttonNavs {
    display: flex;
  }

  .kids {
    margin: auto;
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
          // this.apiUrls = response.data.apiUrl;
          console.log("HERE ARE YOUR PICS");
          console.log(this);
        }.bind(this)
      );



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
        console.log("CURRENT STATUS:");
        console.log(category.currentArticleVisible);
        category.currentArticleVisible = !category.currentArticleVisible;
        console.log("NEW STATUS:");
        console.log(category.currentArticleVisible);
        console.log(this);
      },
      // need to figure out how to get this to change
    },
    computed: {}
  };
</script>
