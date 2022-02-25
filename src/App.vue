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
  <nav class="navbar navbar-expand-lg navbar-light bg-light navbar navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" to="/">Bens Movie List</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarTogglerDemo02"
        aria-controls="navbarTogglerDemo02"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarTogglerDemo02">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link v-if="!!isLoggedIn" class="nav-link" to="/movies">Movies</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="!!isLoggedIn" class="nav-link" to="/movies/new">Add Movies</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="!isLoggedIn" class="nav-link" to="/signup">Signup</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="!isLoggedIn" class="nav-link" to="/login">Login</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="!!isLoggedIn" class="nav-link" to="/logout">Logout</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <router-view />
</template>
