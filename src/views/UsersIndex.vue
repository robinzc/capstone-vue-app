<template>
  <div class="users-index">
    <div>
      Search by name: <input type="text" v-model="nameFilter" list="names" />
      <datalist id="names">
        <option v-for="user in users"
          >{{ user.first_name }} {{ user.last_name }}</option
        >
      </datalist>
    </div>
    <h2>The Travel Universe</h2>
    <h4>
      Find your travel network. Connect to your friends in order to build your
      universe and inform your travels with trusted advice.
    </h4>
    <div
      v-for="user in orderBy(
        filterBy(users, nameFilter, 'last_name', 'first_name'),
        'last_name'
      )"
    >
      <router-link :to="`/users/${user.id}`"></router-link>
      <div v-if="!user.accepted_friend">
        <h2>{{ user.first_name }} {{ user.last_name }}</h2>
        <h5>{{ user.email }}</h5>
        <h5>{{ user.languages_spoken }}</h5>
        <span class="image main"><img :src="user.image_url" alt=""/></span>
        <br />
        <router-link :to="`/users/${user.id}`">Profile</router-link>
        <br />
        <span
          v-if="user.accepted_friend != true && user.pending_friend != true"
        >
          <button v-on:click="createConnection(user)">
            Request to Connect
          </button>
        </span>
        <br />
      </div>
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
      nameFilter: "",
    };
  },
  created: function() {
    axios.get("/api/users").then((response) => {
      console.log(response.data);
      this.users = response.data;
    });
  },
  methods: {
    createConnection: function(user) {
      var params = {
        recipient_id: user.id,
      };
      axios
        .post("/api/connections", params)
        .then((response) => {
          this.$router.push("/connections");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>
