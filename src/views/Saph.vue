<template>
  <div class="home">
    <h2>No Ruby Calls</h2>
    <div>
      <button v-on:click="counter(num)">Press Me</button>
      <h2>{{  num  }}</h2>
    </div>  
<!--     <div v-for="art in articles">
      <div class="article_img">
        <h2>{{  art.title  }}</h2>
        <h3>{{  art.author  }}</h3>
        <img v-bind:src="art.master_image" alt = "">
        <p v-html="art.body"></p>
      </div>
      <button>Press button</button>
    </div> -->
  </div>
</template>

<style>
/*  .article_img img {
    display: block;
    max-width: 500px;
    max-height: 300px;
  }*/

</style>
<script>
var axios = require("axios");
export default {
  data: function() {
    // var key = process.env.VUE_APP_MY_API_KEY;
    // results: [];
    return {
      info: null
    };
  },
  // need to find out about the API KEY. DO NOT INCLUDE IN COMMIT!!
  //   console.log(process.env.VUE_APP_MY_API_KEY);
  created: function() {
    console.log("Ready to call the API!");
    var results = axios.get("https://content.guardianapis.com/sport?&api-key=APIKEY").then(response => this.info = response.data.response.results[0].apiUrl);
    console.log(results);
    console.log("Call complete");
  },

  methods: {
    counter: function() {
      var num = 0;
      num += 1;
      console.log(num);
    }

  },
  computed: {

  }
};
</script>
