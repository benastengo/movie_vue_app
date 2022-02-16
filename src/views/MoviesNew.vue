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
    title:
    <input type="text" v-model="newMovieParams.title" />
    year:
    <input type="text" v-model="newMovieParams.year" />
    plot:
    <input type="text" v-model="newMovieParams.plot" />
    <small class="danger" v-if="newMovieParams.plot.length < 30 && newMovieParams.plot.length > 0">
      Plot must be greater than 30 characters
    </small>
    director:
    <input type="text" v-model="newMovieParams.director" />
    english:
    <input type="text" v-model="newMovieParams.english" />
    <button v-on:click="newMovie()">Update Movie</button>
  </div>
</template>

<style>
.danger {
  color: rgb(252, 0, 0);
}
</style>
