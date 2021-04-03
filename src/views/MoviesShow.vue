<template>
  <div class="movies-show">
    <h1>{{ message }}</h1>
    <div class="container">
      <h1 class="title">{{ movie.title }}</h1>
      <p>
        Plot:
        {{ movie.plot }}
        <br />
        Director:
        {{ movie.director }}
        <br />
        Year:
        {{ movie.year }}
        <br />
      </p>
      <button v-on:click="destroyMovie(movie)" type="button" class="btn btn-danger">Delete</button>
      <button v-on:click="showMovie(movie)" type="button" class="btn btn-info">Update</button>
    </div>
    <!-- <router-link v-bind:to="`/movies/${recipe.id}/edit`">See more info</router-link> -->
    <div>
      <dialog id="movie-details">
        <form method="dialog">
          <h2>Movie</h2>
          <p>
            Title:
            <input type="text" v-model="movie.title" />
          </p>
          <p>
            Plot:
            <input type="text" v-model="movie.plot" />
          </p>
          <p>
            Director:
            <input type="text" v-model="movie.director" />
          </p>
          <p>
            Year:
            <input type="text" v-model="movie.year" />
          </p>
          <button>Close</button>
          <button v-on:click="updateMovie(movie)">Update Movie</button>
        </form>
      </dialog>
    </div>
  </div>
</template>
<style>
.container {
}
.title {
  margin: 0.5em 0;
  color: blueviolet;
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
    axios.get("/api/movies/" + this.$route.params.id).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    // showMovie: function () {
    //   axios.get("/api/movies/" + this.$route.params.id).then((response) => {
    //     console.log(response.data);
    //     this.movie = response.data;
    //   });
    // },
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
    showMovie: function (movie) {
      console.log(movie);
      this.currentmovie = movie;
      document.querySelector("#movie-details").showModal();
    },
  },
};
</script>
