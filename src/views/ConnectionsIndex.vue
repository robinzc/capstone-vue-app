<template>
  <div class="connections-index">
    <h2>Your Universe</h2>
    <div v-for="connection in connections">
      <h2>Sender: {{ connection.sender_id }}</h2>
      <h4>Recipient: {{ connection.recipient_id }}</h4>
      <h5>Accepted: {{ connection.accepted }}</h5>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      connections: [
        {
          first_name: "",
          last_name: "",
          email: "",
          languages_spoken: "",
          image_url: "",
        },
      ],
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
