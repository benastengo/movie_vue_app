<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
      editMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log("movies show", response);
      this.movie = response.data;
      this.editMovieParams = this.movie;
    });
  },
  methods: {
    updateMovie: function (movie) {
      axios
        .patch(`/movies/${movie.id}`, movie)
        .then((response) => {
          console.log("Success!", response.data);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>

<template>
  <div class="movies-edit">
    <h1>Edit movie</h1>
    <form v-on:submit.prevent="updateMovie(movie)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="editMovieParams.title" />
      plot:
      <input type="text" v-model="editMovieParams.plot" />
      year:
      <input type="text" v-model="editMovieParams.year" />
      director:
      <input type="text" v-model="editMovieParams.director" />
      english:
      <input type="text" v-model="editMovieParams.english" />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>
