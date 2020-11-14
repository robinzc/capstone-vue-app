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
        <h4 v-if="connection.accepted">Connected</h4>
        <h4 v-if="!connection.accepted">Connection request pending</h4>
        <span v-if="connection.accepted != true">
          <button
            v-if="connection.recipient_id == $parent.getUserId()"
            v-on:click="updateConnection(connection)"
          >
            Accept connection request
          </button>
        </span>
        <button>
          <router-link :to="`/users/${connection.user.id}`"
            >Profile</router-link
          >
        </button>
        <br />
        <span v-if="connection.accepted">
          <button v-on:click="destroyConnection(connection)">
            Delete this connection
          </button>
        </span>
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
  methods: {
    updateConnection: function(connection) {
      axios
        .patch(`/api/connections/${connection.id}`)
        .then((response) => {
          this.$router.push(`/users/${connection.sender_id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyConnection: function(connection) {
      if (confirm("Are you sure you want to delete this connection?"));
      {
        axios.delete(`/api/connections/${connection.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/users");
        });
      }
    },
  },
};
</script>
