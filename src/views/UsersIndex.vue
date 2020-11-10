<template>
  <div class="users-index">
    <h2>The Travel Universe</h2>
    <h4>
      Find your travel network. Connect to your friends in order to build your
      universe and inform your travels with trusted advice.
    </h4>
    <div v-for="user in users">
      <h2>{{ user.first_name }} {{ user.last_name }}</h2>
      <h5>{{ user.email }}</h5>
      <h5>{{ user.languages_spoken }}</h5>
      <span class="image main"><img :src="user.image_url" alt=""/></span>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      users: [],
    };
  },
  created: function() {
    axios.get("/api/users").then((response) => {
      console.log(response.data);
      this.users = response.data;
    });
  },
  methods: {},
};
</script>
