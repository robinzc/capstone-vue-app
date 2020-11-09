<template>
  <div class="users-edit">
    <form v-on:submit.prevent="updateUser()">
      <h1>My Profile</h1>
      <h2>{{ user.first_name }} {{ user.last_name }}</h2>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Email:</label>
        <input type="text" class="form-control" v-model="user.email" />
      </div>
      <div class="form-group">
        <label>Languages Spoken:</label>
        <input
          type="text"
          class="form-control"
          v-model="user.languages_spoken"
        />
      </div>
      <div class="form-group">
        <label>Picture:</label>
        <input type="text" class="form-control" v-model="user.image_url" />
      </div>
      <input type="submit" class="btn btn-primary" value="Update" />
    </form>
    <div>
      <h3>
        Complete your profile by selecting the cities you have visited or lived
        in.
      </h3>
    </div>
    <div>
      <label class="typo__label">First choose your cities:</label>
      <multiselect
        v-model="value"
        :options="cityOptions"
        :multiple="true"
        :close-on-select="false"
        :clear-on-select="false"
        :preserve-search="true"
        placeholder="Select your cities"
        label="name"
        track-by="name"
        :preselect-first="true"
      >
        <template slot="selection" slot-scope="{ values, isOpen }"
          ><span
            class="multiselect__single"
            v-if="values.length &amp;&amp; !isOpen"
            >{{ values.length }} cities selected</span
          ></template
        >
      </multiselect>
      <!-- <pre class="language-json"><code>{{ value  }}</code></pre> -->
      <div v-for="city in value">
        <p>{{ city.name }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Multiselect from "vue-multiselect";

export default {
  components: { Multiselect },
  data: function() {
    return {
      user: {},
      errors: [],
      value: [],
      cityOptions: [
        { name: "San Francisco, USA" },
        { name: "Shanghai, China" },
        { name: "Karachi, Pakistan" },
        { name: "Prague, Czechia" },
        { name: "Istanbul, Turkey" },
        { name: "Berlin, Germany" },
      ],
    };
  },
  // created: function () {
  //   axios.get("api/user_cities").then((response) => {
  //     this.tags = response.data;
  //     console.log(response.data)
  //   });
  // },

  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
    });
  },
  methods: {
    updateUser: function() {
      var params = {
        email: this.user.email,
        languages_spoken: this.user.languages_spoken,
        image_url: this.user.image_url,
      };
      axios
        .patch(`/api/users/${this.user.id}`, params)
        .then((response) => {
          this.$router.push(`/users/${this.user.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    addNewCityAssociation: function() {
      this.city.push(this.newCityAssociation);
      this.newCityAssociation = "";
    },
  },
};
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

// Needs city association data // Multiselect experiment...
