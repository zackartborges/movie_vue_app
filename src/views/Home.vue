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
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome tweeo Vue.js!",
      movies: [],
      // currentMovie: {},
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
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
      axios.post("/api/movies", params).then((response) => {
        console.log("Successfully added movie!", response.data);
        this.movies.push(response.data);
      });
    },
  },
};
</script>
