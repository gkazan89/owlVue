<template>
  <div class="home">
    <h1>Articles</h1>
    <div>
      <!-- Put cube right here -->
      <div class="bigbox">
        <!-- fuse the cube with the article text -->
        <div class="radio-group" v-on:click="changeSide">
          <div v-for="categoryWithSide in categoriesWithSides">
            <label>
              <input type="radio" name="rotate-cube-side" v-bind:value="categoryWithSide.side"/> {{categoryWithSide.category.category}}
            </label>
          </div>
        </div>  
        <div class="scene">
          <div class="cube">
            <div v-for="categoryWithSide in categoriesWithSides">
              <div v-bind:class="'cube__face cube__face--'+categoryWithSide.side">
                <p>{{categoryWithSide.category.category}}</p>
                <p>{{ categoryWithSide.category.data[categoryWithSide.category.currentArticleIndex].webTitle }}</p>
                <div>
                  <p v-if="categoryWithSide.category.currentArticleVisible" v-html="info.response.content.blocks.body[0].bodyHtml"></p>
                </div>
                <div class="buttons">
                  <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored" v-on:click="upOne(categoryWithSide.category)">Up One</button>
                  <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--accent" v-on:click="downOne(categoryWithSide.category)">Down One</button>
                  <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored" id="show-dialog" v-on:click="read(categoryWithSide.category)">READ</button>
                  <button class="mdl-button mdl-js-button mdl-button--raised mdl-button--accent" v-on:click="visible(categoryWithSide.category)">VISIBLE</button>
                </div>
              </div>
            </div>
          </div>
        </div>

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

  .bigbox {
    box-sizing: border-box;
  }

  .scene {
    width: 500px;
    height: 500px;
    border: 1px solid #ccc;
    margin: 100px;
    perspective: 600px;
  }

  .cube {
    width: 100%;
    height: 100%;
    position: relative;
    transform-style: preserve-3d;
    transform: translateZ(-250px);
    transition: transform 1s;
  }

  .cube.show-front {
    transform: translateZ(-250px) rotateY(0deg);
  }
  .cube.show-right {
    transform: translateZ(-250px) rotateY(-90deg);
  }
  .cube.show-back {
    transform: translateZ(-250px) rotateY(-180deg);
  }
  .cube.show-left {
    transform: translateZ(-250px) rotateY(90deg);
  }
  .cube.show-top {
    transform: translateZ(-250px) rotateX(-90deg);
  }
  .cube.show-bottom {
    transform: translateZ(-250px) rotateX(90deg);
  }

  .cube__face {
    position: absolute;
    width: 500px;
    height: 500px;
    border: 2px solid black;
    line-height: 500px;
    font-size: 40px;
    font-weight: bold;
    color: white;
    text-align: center;
  }


  .cube__face--front {
    background: hsla(0, 100%, 50%, 0.7);
  }
  .cube__face--right {
    background: hsla(60, 100%, 50%, 0.7);
  }
  .cube__face--back {
    background: hsla(120, 100%, 50%, 0.7);
  }
  .cube__face--left {
    background: hsla(180, 100%, 50%, 0.7);
  }
  .cube__face--top {
    background: hsla(240, 100%, 50%, 0.7);
  }
  .cube__face--bottom {
    background: hsla(300, 100%, 50%, 0.7);
  }

  .cube__face--front {
    transform: rotateY(0deg) translateZ(250px);
  }
  .cube__face--right {
    transform: rotateY(90deg) translateZ(250px);
  }
  .cube__face--back {
    transform: rotateY(180deg) translateZ(250px);
  }
  .cube__face--left {
    transform: rotateY(-90deg) translateZ(250px);
  }
  .cube__face--top {
    transform: rotateX(90deg) translateZ(250px);
  }
  .cube__face--bottom {
    transform: rotateX(-90deg) translateZ(250px);
  }

  label {
    margin-right: 10px;
  }

</style>


<script>
// set initial side
// changeSide();

// radioGroup.addEventListener("change", changeSide);
// end of all the cube js

var axios = require("axios");
export default {
  data: function() {
    return {
      categories: [],
      info: [],
      cube: null,
      radioGroup: null,
      currentClass: "",
      categoriesWithSides: []
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

        var sides = ["front", "right", "back", "left", "top", "bottom"];
        var index = 0;
        this.categories.forEach(category => {
          this.categoriesWithSides.push({
            category: category,
            side: sides[index]
          });
          index += 1;
        });

        // this.categoriesWithSides = this.categories.map(category => {category: category.category, })
      }.bind(this)
    );
    console.log("HELLO!!!");
    console.log(this);
    console.log("-------");

    // var other = axios.get();
  },
  mounted: function() {
    // all the js for the cube
    this.cube = document.querySelector(".cube");
    this.radioGroup = document.querySelector(".radio-group");
    this.currentClass = "";
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
    // need to figure out how to get this to change
    visible: function(category) {
      console.log("CURRENT STATUS:");
      console.log(category.currentArticleVisible);
      category.currentArticleVisible = !category.currentArticleVisible;
      console.log("NEW STATUS:");
      console.log(category.currentArticleVisible);
    },
    // cube code
    changeSide: function(event) {
      var checkedRadio = this.radioGroup.querySelector(":checked");
      var showClass = "show-" + checkedRadio.value;
      if (this.currentClass) {
        this.cube.classList.remove(this.currentClass);
      }
      this.cube.classList.add(showClass);
      this.currentClass = showClass;
    }
  },
  computed: {}
};
</script>
