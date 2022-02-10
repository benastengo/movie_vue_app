<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      newMovies: {},
      editMovie: {},
      movieInfo: {},
    };
  },
  created: function () {
    this.moviesIndex();
  },
  methods: {
    moviesIndex: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log("Sanity", response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      axios.post("http://localhost:3000/movies", this.newMovies).then((response) => {
        console.log("sanity", response);
        this.movies.push(response.data);
        this.newMovies = {};
      });
    },
    showInfo: function (movie) {
      this.movieInfo = movie;
      this.editMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      axios.patch(`http://localhost:3000/movies/${movie.id}`, this.editMovie).then((response) => {
        console.log(response);
        this.movieInfo;
      });
    },
    destroyMovie: function (movie) {
      axios.delete(`localhost:3000/movies/${movie.id}`).then((response) => {
        console.log("RIP", response);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>Movies, Y'all</h1>
    <div>
      Title:
      <input type="text" v-model="newMovies.title" />
      Year:
      <input type="text" v-model="newMovies.year" />
      Plot:
      <input type="text" v-model="newMovies.plot" />
      Director:
      <input type="text" v-model="newMovies.director" />
      English:
      <input type="text" v-model="newMovies.english" />
      <button v-on:click="createMovie()">Create</button>
    </div>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <p>{{ movie.title }}</p>
      <button v-on:click="showInfo(movie)">Show Info</button>
      <div v-if="movie.id === movieInfo.id">
        Movie year: {{ movieInfo.year }}
        <br />
        Movie director: {{ movieInfo.director }}
        <br />
        Movie plot: {{ movieInfo.plot }}
        <br />
        <div></div>
      </div>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h3>``~~((UPDATE MOVIE)~~``</h3>
        <label for="title">Title:</label>
        <input type="text" v-model="movieInfo.title" id="title" />
        <br />
        <label for="title">Year:</label>
        <input type="number" v-model="movieInfo.year" min="1800" max="2022" id="year" />
        <br />
        <label for="title">Plot:</label>
        <input type="text" v-model="movieInfo.plot" id="plot" />
        <br />
        <label for="title">Director:</label>
        <input type="text" v-model="movieInfo.director" id="director" />
        <br />
        <label for="title">English?</label>
        <input type="text" v-model="movieInfo.english" id="english" />
        <br />
        <button v-on:click="updateMovie(movieInfo)">Update Movie</button>
        <button v-on:click="destroyMovie(movieInfo)">Kill-Switch</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>
