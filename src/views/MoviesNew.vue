<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Add some movies!",
      newMovieParams: { plot: "" },
      errors: [],
    };
  },
  created: function () {},
  methods: {
    newMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log("New Movies", response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("photos create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="Movies-New">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
    </ul>
    <form action="">
      <label for="Title">title:</label>
      <input type="text" v-model="newMovieParams.title" />
      <label for="Year">year:</label>
      <input type="text" v-model="newMovieParams.year" />
      <label for="Plot">plot:</label>
      <input type="text" v-model="newMovieParams.plot" />
      <small class="danger" v-if="newMovieParams.plot.length < 30 && newMovieParams.plot.length > 0">
        Plot must be greater than 30 characters
      </small>
      <label for="Director">Director:</label>
      <input type="text" v-model="newMovieParams.director" />
      <label for="English">english:</label>
      <input type="checkbox" v-model="newMovieParams.english" />
      <button v-on:click="newMovie()"><strong>CREATE!!!!!!</strong></button>
    </form>
  </div>
</template>

<style>
.danger {
  color: rgb(255, 5, 5);
}
</style>
