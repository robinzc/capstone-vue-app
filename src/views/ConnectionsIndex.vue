<template>
  <div class="connections-index">
    <div>
      Search by name: <input type="text" v-model="nameFilter" list="names" />
      <datalist id="names">
        <option v-for="connection in connections"
          >{{ connection.user.first_name }}
          {{ connection.user.last_name }}</option
        >
      </datalist>
    </div>
    <h1>Your Universe</h1>
    <button>
      <router-link :to="`/map_connections`">
        See your connections map</router-link
      >
    </button>
    <div
      v-for="connection in orderBy(
        filterBy(connections, nameFilter, 'user.last_name', 'user.first_name'),
        'accepted'
      )"
    >
      <div>
        <h2>
          {{ connection.user.first_name }}
          {{ connection.user.last_name }}
        </h2>
        <span class="image main"
          ><img :src="connection.user.image_url" alt=""
        /></span>
        <h5>Email: {{ connection.user.email }}</h5>
        <h5>Languages: {{ connection.user.languages_spoken }}</h5>
        <h4 v-if="!connection.accepted">Connection pending</h4>
        <button>
          <router-link :to="`/users/${connection.user.id}`"
            >Profile</router-link
          >
        </button>
        <!-- Confirmed connections need an update/accept button -->
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
      connections: [],
      nameFilter: "",
    };
  },
  created: function() {
    axios.get("/api/connections").then((response) => {
      console.log(response.data);
      this.connections = response.data;
    });
  },
  methods: {},
};
</script>
