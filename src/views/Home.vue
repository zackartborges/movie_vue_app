<template>
  <div class="home">
    <div class="jumbotron">
      <h1 class="display-4">WELCOME TO THE MOVIE WEBSITE!</h1>
      <p class="lead">THIS IS WHERE YOU SEE MOVIE STUFF</p>
      <hr class="my-4" />
      <p>SO nice to have you.</p>
      <a class="btn btn-warning btn-lg" href="/movies" role="button">See All Movies</a>
    </div>
    <br />
    <h2>Thank you for coming to my website. Don't forget to tip your waiter!</h2>
  </div>
</template>
<style>
body {
  background-color: blanchedalmond !important
;
}
</style>
<script>
import axios from "axios";
// import func from "vue-editor-bridge";
export default {
  data: function () {
    return {
      message: "Welcome to the home page!",
      movies: [],
      currentMovie: {},
      errors: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then((response) => {
        this.movies = response.data;
        console.log("all movies:", this.movies);
      });
    },
    createMovie: function () {
      console.log("adding movie..");
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
      };
      axios
        .post("/api/movies", params)
        .then((response) => {
          console.log("Successfully added movie!", response.data);
          this.movies.push(response.data);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    destroyMovie: function (movie) {
      axios.delete("/api/movies/" + movie.id).then((response) => {
        console.log("Success!", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
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
