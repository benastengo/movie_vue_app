<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Movies!",
      movies: [],
      newMovies: {},
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
    showInfo: function (id) {
      axios.get(`http://localhost:3000/movies/${id}`).then((response) => {
        this.movieInfo = response.data;
        this.id = this.movieInfo.id;
      });
    },
    updateMovie: function (id) {
      axios.patch(`http://localhost:3000/movies/${id}`, this.movieInfo).then((response) => {
        this.movies.forEach((movie, index) => {
          if (movie.id == response.data.id) {
            movie = response.data;
            this.movies[index] = response.data;
          }
        });
      });
    },
    destroyMovie: function (movie) {
      axios.delete(`localhost:3000/movies/${movie.id}`).then((response) => {
        console.log("RIP", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
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
      <button v-on:click="showInfo(movie.id)">Show Info</button>
      <div v-if="movie.id === movieInfo.id">
        Movie year: {{ movieInfo.year }}
        <br />
        Movie director: {{ movieInfo.director }}
        <br />
        Movie plot: {{ movieInfo.plot }} Movie
        <br />
        <div>
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
          <input type="checkbox" v-model="movieInfo.english" id="english" />
          <br />
          <button v-on:click="updateMovie(id)">Update Movie</button>
          <button v-on:click="destroyMoive(movie.id)">Kill-Switch</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
