<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
      Title:
      <input type="text" v-model="newMovieTitle" />
      Year:
      <input type="text" v-model="newMovieYear" />
      Plot:
      <input type="text" v-model="newMoviePlot" />
      Director:
      <input type="text" v-model="newMovieDirector" />
      <button v-on:click="createMovie">Add a Movie!</button>
    </div>
    <div v-for="movie in movies" v-bind:key="movie">
      <h1>{{ movie.title }}</h1>
      <button v-on:click="showMovie(movie)">More info!</button>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
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
        <button v-on:click="updateMovie(currentMovie)">Update Movie Info</button>
        <button v-on:click="destroyMovie(currentMovie)">Terminate Movie</button>
        <button>Close</button>
      </form>
    </dialog>
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
      movies: [],
      currentMovie: {},
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
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
