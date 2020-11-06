<template>
  <div class="users-show">
    <h1>Profile</h1>
    <h2>{{ user.first_name }} {{ user.last_name }}</h2>
    <img :src="user.image_url" alt="" />
    <h5>{{ user.email }}</h5>
    <h5>{{ user.languages_spoken }}</h5>
    <h5>{{ user.user_cities }}</h5>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      user: {},
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
    });
  },
  methods: {},
};
</script>

// Needs city association data
