<script>
export default {
  data: function () {
    return {
      isLoggedIn: !!localStorage.jwt,
    };
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
      this.flashMessage = localStorage.flashMessage;
      localStorage.removeItem("flashMessage");
    },
  },
};
</script>

<template>
  <div id="nav">
    <router-link to="/">Home</router-link>
    |
    <router-link v-if="!isLoggedIn" to="/signup">Signup</router-link>
    |
    <router-link v-if="!isLoggedIn" to="/login">Login</router-link>
    |
    <router-link v-if="!!isLoggedIn" to="/logout">Logout</router-link>
    |
    <router-link v-if="!!isLoggedIn" to="/movies">Movies</router-link>
    |
    <router-link v-if="!!isLoggedIn" to="/movies/new">New Movie</router-link>
  </div>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffb700;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #fcfcfc;
}

#nav a.router-link-exact-active {
  color: #ffffff;
}

#wrapper {
  width: auto;
  height: auto;
  background-color: rgb(250, 0, 0);
  margin: 0 auto;
  margin-top: auto;
  border-radius: auto;
}
html,
body {
  margin: auto;
  padding: auto;
  background-color: rgb(0, 0, 0);
}
</style>
