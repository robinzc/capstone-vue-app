<template>
  <div class="users-show">
    <h1>Profile</h1>
    <button>
      <router-link :to="`/map_connections`">
        See your connections map</router-link
      >
    </button>
    <h2>{{ user.first_name }} {{ user.last_name }}</h2>
    <img :src="user.image_url" alt="" />
    <h5>Contact me: {{ user.email }}</h5>
    <h5>My languages: {{ user.languages_spoken }}</h5>

    <h3>My Cities</h3>

    <div v-for="associated_city in user.associated_cities">
      <h4>{{ associated_city.city_name }}</h4>
      <p v-if="associated_city.current_living">I'm living here</p>
      <p v-if="associated_city.current_visiting">I'm visiting here</p>
      <p v-if="associated_city.lived">I've lived here</p>
      <p v-if="associated_city.visited">I've visited here</p>
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
    });
  },
  methods: {},
};
</script>

// Needs friend validation // this.associated_cities =
this.user.associated_cities.map((city) => { // return { id: city.city_id, name:
city.city_name }; // }); // this.user.associated_cities.forEach((city) => { //
if (city.current_living) { // this.associated_cities.push({ // city_id:
city.city_id, // current_living: true, // }); // } // if (city.current_visiting)
{ // this.associated_cities.push({ // city_id: city.city_id, //
current_visiting: true, // }); // } // if (city.visited) { //
this.associated_cities.push({ // city_id: city.city_id, // visited: true, // });
// } // if (city.lived) { // this.associated_cities.push({ // city_id:
city.city_id, // lived: true, // }); // } // });n
