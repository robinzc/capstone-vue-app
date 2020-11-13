<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Sign Up with Traverse</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>First name:</label>
        <input type="text" class="form-control" v-model="first_name" />
      </div>
      <div class="form-group">
        <label>Last name:</label>
        <input type="text" class="form-control" v-model="last_name" />
      </div>
      <div class="form-group">
        <label>Email:</label>
        <input type="email" class="form-control" v-model="email" />
      </div>
      <div class="form-group">
        <label>Password:</label>
        <input type="password" class="form-control" v-model="password" />
      </div>
      <div class="form-group">
        <label>Password confirmation:</label>
        <input
          type="password"
          class="form-control"
          v-model="passwordConfirmation"
        />
      </div>
      <div class="form-group">
        <label>What languages do you speak?</label>
        <input type="text" class="form-control" v-model="languages_spoken" />
      </div>
      <div class="form-group">
        <label>Please enter a profile picture: </label>
        <input type="url" class="form-control" v-model="image_url" />
      </div>
      <input type="submit" class="btn btn-primary" value="Sign up!" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      first_name: "",
      last_name: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      languages_spoken: "",
      image_url: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        first_name: this.first_name,
        last_name: this.last_name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
        languages_spoken: this.languages_spoken,
        image_url: this.image_url,
      };

      axios
        .post("/api/users", params)
        .then((response) => {
          axios.post("/api/sessions", params).then((response) => {
            axios.defaults.headers.common["Authorization"] =
              "Bearer " + response.data.jwt;
            localStorage.setItem("jwt", response.data.jwt);
            localStorage.setItem("user_id", response.data.user_id);
            this.$router.push(`/users/${response.data.user_id}/edit`);
          });
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
