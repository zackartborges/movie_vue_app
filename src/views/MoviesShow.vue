<template>
  <div class="movies-show">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-bind:key="movie">
      <h1>{{ movie.title }}</h1>
    </div>
    <div>
      <!-- <dialog id="movie-details"> -->
      <!-- <form method="dialog"> -->
      <h1>Movie Info</h1>
      <p>
        Title:
        <input type="text" v-model="currentMovie.title" />
      </p>
      <p>
        Year:
        <input type="text" v-model="currentMovie.year" />
      </p>
      <p>
        Plot:
        <input type="text" v-model="currentMovie.plot" />
      </p>
      <p>
        Director:
        <input type="text" v-model="currentMovie.director" />
      </p>
    </div>
    <!-- </form> -->
    <!-- </dialog> -->
  </div>
</template>
<style>
body {
  background-color: blanchedalmond;
}
</style>
<script>
import axios from "axios";
// import func from "vue-editor-bridge";
export default {
  data: function () {
    return {
      message: "Welcome tweeo Vue.js!",
      // movies: [],
      currentMovie: {},

      errors: [],
    };
  },
  created: function () {
    this.showMovie();
  },
  methods: {
    showMovie: function () {
      axios.get("/api/movies/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.movie = response.data;
      });
    },
    // destroyMovie: function (movie) {
    //   axios.delete("/api/movies/" + movie.id).then((response) => {
    //     console.log("Success!", response.data);
    //     var index = this.movies.indexOf(movie);
    //     this.movies.splice(index, 1);
    //   });
    // },
    // updateMovie: function (movie) {
    //   var params = {
    //     title: movie.title,
    //     year: movie.year,
    //     plot: movie.plot,
    //     director: movie.director,
    //   };
    //   axios.patch("/api/movies/" + movie.id, params).then((response) => {
    //     console.log("Succeeeesss!!", response.data);
    //   });
    // },
  },
};
</script>
