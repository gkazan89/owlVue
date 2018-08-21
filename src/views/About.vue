<template>
  <div class="about">
    <h2>Category Select</h2>
    <div v-for="cat in categories">
      <ul>
        <input type="checkbox" v-model="checkedNames">
        <label for><ol>{{cat.name}}</ol></label>
      </ul>  
    </div>
    <div id="cats">Checked categories: {{  checkedNames  }}</div>
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

  methods: {
  },
  computed: {}
};

</script>