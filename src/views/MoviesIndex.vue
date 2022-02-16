<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Movies index",
      movies: [],
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log("Sanity", response.data);
      this.movies = response.data;
    });
  },
  methods: {
    moviesIndex: function (movie) {
      this.$router.push(`/movies/${movie.id}`);
    },
  },
};
</script>

<template>
  <div class="home">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h1>{{ movie.title }}</h1>
      <router-link v-bind:to="`/movies/${movie.id}`">More details</router-link>
    </div>
  </div>
</template>

<style></style>
