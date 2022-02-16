<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Movies index",
      movies: [],
      titleFilter: "",
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
  computed: {
    filteredMovies() {
      return this.movies.filter((movie) => {
        return movie.title.toLowerCase().includes(this.titleFilter.toLowerCase());
      });
    },
  },
};
</script>

<template>
  <div class="Movies-index">
    <p>
      Search By Title:
      <input type="text" v-model="titleFilter" list="titles" />
    </p>
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">
        {{ movie.title }}
      </option>
    </datalist>
    <div v-for="movie in filteredMovies" v-bind:key="movie.id">
      <h1>{{ movie.title }}</h1>
      <router-link v-bind:to="`/movies/${movie.id}`">More details</router-link>
    </div>
  </div>
</template>

<style></style>
