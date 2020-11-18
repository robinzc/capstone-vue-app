<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand" href="#x"
          ><img
            src="assets/images/logo.svg
          "
            alt=""
        /></a>

        <button
          class="navbar-toggler collapsed"
          type="button"
          data-toggle="collapse"
          data-target="#navbar-toggle1"
          aria-controls="navbar-toggle1"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="icon-bar top-bar"></span>
          <span class="icon-bar middle-bar"></span>
          <span class="icon-bar bottom-bar"></span>
          <span class="sr-only">Toggle navigation</span></button
        ><!-- / navbar-toggler -->

        <div class="collapse navbar-collapse" id="navbar-toggle1">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item" v-if="!isLoggedIn()">
              <router-link class="nav-link active" to="/">
                Welcome
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link active" to="/about">
                About</router-link
              >
            </li>
            <li class="nav-item" v-if="isLoggedIn()">
              <router-link class="nav-link active" to="/users">
                The Universe
              </router-link>
            </li>
            <li class="nav-item" v-if="isLoggedIn()">
              <router-link class="nav-link active" to="/connections">
                Connections</router-link
              >
            </li>
            <li class="nav-item" v-if="isLoggedIn()">
              <router-link
                class="nav-link active"
                v-bind:to="`/users/${getUserId()}`"
              >
                My Profile</router-link
              >
            </li>
            <li class="nav-item" v-if="isLoggedIn()">
              <router-link class="nav-link active" to="/map_connections">
                My Map</router-link
              >
            </li>
            <li class="nav-item" v-if="isLoggedIn()">
              <router-link class="nav-link active" to="/logout">
                Logout</router-link
              >
            </li>
            <!-- / dropdown -->
          </ul>
          <!-- / navbar-nav -->

          <ul class="navbar-button ml-30 m-0 p-0">
            <li class="nav-item" v-if="!isLoggedIn()">
              <router-link class="btn btn-primary btn-sm" to="/login">
                Login</router-link
              >
            </li>
          </ul>
          <ul class="navbar-button ml-30 m-0 p-0">
            <li class="nav-item" v-if="!isLoggedIn()">
              <router-link class="btn btn-primary btn-sm" to="/signup">
                Signup
              </router-link>
            </li>
          </ul>
          <!-- / btn-sm -->
        </div>
        <!-- / navbar-collapse -->
      </div>
      <!-- / container -->
    </nav>
    <!-- / navbar -->

    <router-view :key="$route.path" />
  </div>
</template>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
} */
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      flashMessage: "",
    };
  },
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    },
    getUserId: function() {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
