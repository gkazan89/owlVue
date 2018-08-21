<template>
  <div class="about">
    <h2>Category Select</h2>
    <div v-for="cat in categories">
      <ul>
        <ol>{{cat.name}}</ol>
      </ul>  
    </div>
  </div>
</template>

<script>
var axios = require("axios");
export default {
  data: function() {
    return {
      categories: [],
    };
  },
  created: function() {
    axios.get("http://localhost:3000/api/categories").then(
      function(response) {
        console.log("CATEGORIES:");
        console.log(response);
        this.categories = response.data;
      }.bind(this)
    );
  },

  methods: {},
  computed: {}
};
</script>