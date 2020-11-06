<template>
  <div class="users-new">
    <form v-on:submit.prevent="createUser()">
      <h1>My Profile</h1>
      <!-- <h2>{{ first_name }} {{ last_name }}</h2> -->
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Email:</label>
        <input type="text" class="form-control" v-model="email" />
      </div>
      <div class="form-group">
        <label>Languages Spoken:</label>
        <input type="text" class="form-control" v-model="languages_spoken" />
      </div>
      <div class="form-group">
        <label>Picture:</label>
        <input type="text" class="form-control" v-model="image_url" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      email: "",
      languages_spoken: "",
      image_url: "",
      errors: [],
    };
  },
  methods: {
    createUser: function() {
      var params = {
        email: this.email,
        languages_spoken: this.languages_spoken,
        image_url: this.image_url,
      };
      axios
        .post("/api/users")
        .then((response) => {
          this.$router.push("/users");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
