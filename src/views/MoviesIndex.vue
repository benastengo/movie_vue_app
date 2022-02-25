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
  <div class="container auto">
    <div class="container">
      <div class="row">
        <div class="col">
          <div v-for="movie in movies" v-bind:key="movie.id" class="card bg-dark text-white mt-3 mb-3">
            <img v-bind:src="movie.images[0].url" class="card-img" alt="..." />
            <div class="card-img-overlay">
              <h5 class="card-title">{{ movie.title }}</h5>
              <p class="card-text">{{ movie.plot }}</p>
              <router-link v-bind:to="`/movies/${movie.id}`" class="btn btn-primary">Movie Info</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
