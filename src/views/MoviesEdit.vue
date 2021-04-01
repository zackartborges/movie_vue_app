<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovie(movie)">
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="movie.title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="movie.year" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="movie.plot" />
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="movie.director" />
      </div>
      <input type="submit" class="btn btn -primary" value="submit" />
    </form>
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
      message: "This is The movie!",
      // movies: [],
      movie: {},
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
    updateMovie: function (movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
      };
      axios.patch("/api/movies/" + movie.id, params).then((response) => {
        console.log("Succeeeesss!!", response.data);
      });
    },
  },
};
</script>
