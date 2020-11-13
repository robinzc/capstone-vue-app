<template>
  <div class="connections-map">
    <h1>{{ message }}</h1>
    <!-- <div v-for="friend in friends">
      <div v-for="city in friend.associated_cities">
        {{ city.name }}
        {{ city.longitude }}
        {{ city.latitude }}
        {{ friend.first_name }} {{ friend.last_name }}
      </div>
    </div> -->
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  width: 100%;
  height: 800px;
}

#marker {
  /* background-image: */
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}

.mapboxgl-popup {
  max-width: 200px;
}
</style>

<script>
import axios from "axios";
import mapboxgl from "mapbox-gl";
export default {
  data: function() {
    return {
      message: "Your Travel Universe",
      friends: [],
    };
  },
  mounted: function() {},
  created: function() {
    axios.get("/api/map_connections").then((response) => {
      this.friends = response.data;
      console.log(response.data);
      mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_ACCESS_TOKEN;
      const map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
        center: [-16.6291, 28.2916], // starting position [lng, lat]
        zoom: 1.5, // starting zoom
      });
      this.friends.forEach((friend) => {
        console.log(friend);
        friend.associated_cities.forEach((associated_city) => {
          console.log(
            friend.first_name,
            friend.last_name,
            associated_city.name,
            associated_city.longitude,
            associated_city.latitude
          );
          var popup = new mapboxgl.Popup({ offset: 25 }).setText(
            friend.first_name
          );
          var marker = new mapboxgl.Marker()
            .setLngLat([associated_city.longitude, associated_city.latitude])
            .setPopup(popup)
            .addTo(map);
        });
      });
    });
  },
  methods: {},
};
</script>
// this.associated_cities = this.user.associated_cities.map((city) => { //
return { id: city.city_id, name: city.city_name }; // }); //
this.user.associated_cities.forEach((city) => { // if (city.current_living) { //
this.associated_cities.push({ // city_id: city.city_id, // current_living: true,
// }); // } // if (city.current_visiting) { // this.associated_cities.push({ //
city_id: city.city_id, // current_visiting: true, // }); // } // if
(city.visited) { // this.associated_cities.push({ // city_id: city.city_id, //
visited: true, // }); // } // if (city.lived) { // this.associated_cities.push({
// city_id: city.city_id, // lived: true, // }); // } // }); //
this.associatedCities = this.friendCities.associated_cities.map( // (city) => {
// return { // name: city.name, // longitude: city.longitude, // latitude:
city.latitude, // }; // } // );
