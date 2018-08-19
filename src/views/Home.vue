<template>
  <div class="home">
    <h2>Preferences</h2>
    <div v-for="pref in preferences">
      <p>{{  pref.user_id  }}</p>
      <p>{{  pref.category_id  }}</p>
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
      preferences: []
    };
  },
  created: function() {
    axios.get("http://localhost:3000/api/preferences").then(
      function(response) {
        console.log(response);
        this.preferences = response.data;
      }.bind(this)
    );
  },
  methods: {},
  computed: {}
};
</script>