<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Movies Show Action!",
      movie: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log("movies show", response);
      this.movie = response.data;
    });
  },
  methods: {
    destroyMovie: function (movie) {
      axios.delete("/movies/" + movie.id).then((response) => {
        console.log("movies destroy", response);
        this.$router.push("/movies");
      });
    },
  },
};
</script>

<template>
  <div class="movies-show">
    <h1>{{ movie.title }}</h1>
    <p>{{ movie.plot }}</p>
    <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit Movie</router-link>
    <br />
    <button v-on:click="destroyMovie(movie)">Destroy movie</button>
    <br />
    <router-link to="/movies">Back to all movies</router-link>
  </div>
</template>
