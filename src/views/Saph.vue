<template>
  <div class="home">
    <h2>No Ruby Calls</h2>
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
    console.log(process.env.VUE_APP_MY_API_KEY);
  },

  methods: {
  },
  computed: {}
};
</script>
