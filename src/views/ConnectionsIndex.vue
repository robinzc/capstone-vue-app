<template>
  <div class="connections-index">
    <h1>Your Universe</h1>
    <div v-for="connection in connections">
      <h3>
        {{ connection.connection.first_name }}
        {{ connection.connection.last_name }}
      </h3>
      <span class="image main"
        ><img :src="connection.connection.image_url" alt=""
      /></span>
      <h5>Email: {{ connection.connection.email }}</h5>
      <h5>Languages: {{ connection.connection.languages_spoken }}</h5>
    </div>
    <h1>Pending Connections</h1>
    <div v-for="connection in connections">
      <h3>
        {{ connection.connection.first_name }}
        {{ connection.connection.last_name }}
      </h3>
      <span class="image main"
        ><img :src="connection.connection.image_url" alt=""
      /></span>
      <h5>Email: {{ connection.connection.email }}</h5>
      <h5>Languages: {{ connection.connection.languages_spoken }}</h5>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      connections: [],
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
