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
      <div>
        <h3>
          Complete your profile by selecting the cities you have visited or
          lived in.
        </h3>
      </div>
      <div>
        <label class="typo__label">First choose your cities:</label>
        <multiselect
          v-model="selectedCities"
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
        <!-- {{ selectedCities }} -->
        <h3>
          Next check the box that indicates your knowledge of each city you've
          chosen.
        </h3>
        <div v-for="(city, index) in selectedCities">
          <p>{{ city.name }}</p>
          <input
            type="radio"
            :id="city.id"
            :value="{ city_id: city.id, current_living: true }"
            v-model="cityAssociations[index]"
          />
          <label :for="city">I live here now.</label>
          <br />
          <input
            type="radio"
            :id="city.id"
            :value="{ city_id: city.id, lived: true }"
            v-model="cityAssociations[index]"
          />
          <label :for="city">I used to live here.</label>
          <br />
          <input
            type="radio"
            :id="city.id"
            :value="{ city_id: city.id, visited: true }"
            v-model="cityAssociations[index]"
          />
          <label :for="city">I've visited here.</label>
          <br />
          <input
            type="radio"
            :id="city.id"
            :value="{ city_id: city.id, current_visiting: true }"
            v-model="cityAssociations[index]"
          />
          <label :for="city">I'm visiting here now.</label>
          <br />
        </div>
        <br />
        <!-- <span>Associated cities: {{ cityAssociations }}</span> -->
      </div>
      <br />
      <input type="submit" class="btn btn-primary" value="Update my profile" />
    </form>
    <span v-if="user.id == $parent.getUserId()">
      <button v-on:click="destroyUser(user)">
        Delete my profile
      </button>
    </span>
    <button>
      <router-link :to="`/users/${user.id}`">Cancel</router-link>
    </button>
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
      selectedCities: [],
      cityOptions: [],
      cityAssociations: [],
    };
  },

  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.user = response.data;
      this.selectedCities = this.user.associated_cities.map((city) => {
        return { id: city.city_id, name: city.city_name };
      });
      this.user.associated_cities.forEach((city) => {
        if (city.current_living) {
          this.cityAssociations.push({
            city_id: city.city_id,
            current_living: true,
          });
        }
        if (city.current_visiting) {
          this.cityAssociations.push({
            city_id: city.city_id,
            current_visiting: true,
          });
        }
        if (city.visited) {
          this.cityAssociations.push({
            city_id: city.city_id,
            visited: true,
          });
        }
        if (city.lived) {
          this.cityAssociations.push({
            city_id: city.city_id,
            lived: true,
          });
        }
      });
    });
    axios.get("/api/cities").then((response) => {
      this.cityOptions = response.data;
      console.log(response.data);
    });
  },
  methods: {
    updateUser: function() {
      var params = {
        email: this.user.email,
        languages_spoken: this.user.languages_spoken,
        image_url: this.user.image_url,
        city_associations: this.cityAssociations,
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
    destroyUser: function(user) {
      if (
        confirm(
          "Are you sure you want to delete your profile? You will delete your entire Traverse account and will lose all data."
        )
      ) {
        axios.delete(`/api/users/${user.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/logout");
        });
      }
    },
  },
};
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

// Need to finish city association issues
