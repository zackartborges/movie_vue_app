<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    <div>
      <button>Sort Alphabetically</button>
    </div>
    <br />
    Search by name:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <!-- <div class="jumbotron jumbotron-fluid">
        <div class="container"> -->
      <div class="_card card" style="width: 18rem">
        <!-- <img src="" class="card-img-top" alt="..." /> -->
        <div class="card-body">
          <router-link v-bind:to="`/movies/${movie.id}`" class="display-4">
            <h5 class="card-title">{{ movie.title }}</h5>
          </router-link>

          <p class="card-text">
            {{ movie.plot }}
          </p>
        </div>
      </div>
      <!-- </div>
      </div> -->
      <!-- <router-link v-bind:to="`/movies/${movie.id}`">
        <h1>{{ movie.title }}</h1>
      </router-link> -->
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
.movies_index {
  text-align: center !important;
}
._card {
  margin: 6% 40%;
}
</style>
<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

// import func from "vue-editor-bridge";
export default {
  mixins: [Vue2Filters.mixin],

  data: function () {
    return {
      message: "All Movies",
      movies: [],
      errors: [],
      titleFilter: "",
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
