<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link v-bind:to="`/movies/${movie.id}`">
        <h1>{{ movie.title }}</h1>
      </router-link>
      <p>{{ movie.plot }}</p>
    </div>
    <!-- <dialog id="movie-details">
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
      </form> -->
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
      movies: [],
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
  },
};
</script>
