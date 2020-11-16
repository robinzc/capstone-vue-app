<template>
  <div id="app">
    <div id="nav">
      <ul>
        <span v-if="!isLoggedIn()">
          <router-link to="/"> Welcome |</router-link>
        </span>
        <span>
          <router-link to="/about"> About |</router-link>
        </span>
        <span v-if="!isLoggedIn()">
          <router-link to="/signup"> Signup |</router-link>
        </span>
        <!-- Needs to redirect to UsersNew to populate rest of profile after signing up -->
        <span v-if="!isLoggedIn()">
          <router-link to="/login"> Login |</router-link>
        </span>
        <span v-if="isLoggedIn()">
          <router-link to="/logout"> Logout |</router-link>
        </span>
        <span v-if="isLoggedIn()">
          <router-link to="/users"> The Universe |</router-link>
        </span>
        <span v-if="isLoggedIn()">
          <router-link to="/connections"> Connections |</router-link>
        </span>
        <span v-if="isLoggedIn()">
          <router-link v-bind:to="`/users/${getUserId()}`">
            My Profile |</router-link
          >
        </span>
        <span v-if="isLoggedIn()">
          <router-link to="/map_connections"> My Map</router-link>
        </span>
      </ul>
    </div>
    <router-view />
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
