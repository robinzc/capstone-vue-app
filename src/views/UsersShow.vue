<template>
  <div class="users-show">
    <h1>Profile</h1>
    <h2>{{ user.first_name }} {{ user.last_name }}</h2>
    <img :src="user.image_url" alt="" />
    <h5>{{ user.email }}</h5>
    <h5>{{ user.languages_spoken }}</h5>

    <h3>My Cities</h3>

    <!-- <h4>I live in: {{ user.associated_cities.city_name }}</h4>
    <h4>I'm currently visiting: {{ user.associated_cities.city_name }}</h4>
    <h4>Cites I've visited: {{ user.associated_cities.city_name }}</h4>
    <h3>Cities I have livedin: {{ user.associated_cities.city_name }}</h3>
     -->
    <div v-for="associated_city in user.associated_cities">
      <p>{{ user.associated_cities }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      user: {},
      associated_cities: [],
      user_cities: [],
    };
  },
  created: function() {
    axios.get(`/api/users/${this.$route.params.id}`).then((response) => {
      this.user = response.data;
      console.log(response.data);
      this.associated_cities = this.user.associated_cities.map((city) => {
        return { id: city.city_id, name: city.city_name };
      });
      this.user.associated_cities.forEach((city) => {
        if (city.current_living) {
          this.associated_cities.push({
            city_id: city.city_id,
            current_living: true,
          });
        }
        if (city.current_visiting) {
          this.associated_cities.push({
            city_id: city.city_id,
            current_visiting: true,
          });
        }
        if (city.visited) {
          this.associated_cities.push({
            city_id: city.city_id,
            visited: true,
          });
        }
        if (city.lived) {
          this.associated_cities.push({
            city_id: city.city_id,
            lived: true,
          });
        }
      });
    });
  },
  methods: {},
};
</script>

// Needs city association data and friend validation
