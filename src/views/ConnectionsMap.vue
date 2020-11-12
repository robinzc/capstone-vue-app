<template>
  <div class="connections-map">
    <h1>{{ message }}</h1>
    <!-- <div v-for="associated_city in friendCities.associated_cities">
      <h3>{{ associated_cities }}</h3>
    </div> -->
    <h3>{{ friendCities }}</h3>
    <div id="map"></div>
  </div>
</template>

<style>
#map {
  width: 100%;
  height: 800px;
}
</style>

<script>
import axios from "axios";
import mapboxgl from "mapbox-gl";
export default {
  data: function() {
    return {
      message: "Your Travel Universe",
      cities: [],
      friendCities: [
        // {
        //   long: -122.4194,
        //   lat: 37.7749,
        //   description: "San Francisco",
        // },
      ],
      associated_cities: [],
    };
  },
  mounted: function() {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_ACCESS_TOKEN;
    const map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
      center: [-16.6291, 28.2916], // starting position [lng, lat]
      zoom: 1.5, // starting zoom
    });
    this.friendCities.forEach((friendCity) => {
      var popup = new mapboxgl.Popup({ offset: 25 }).setText(friendCity.name);
      var marker = new mapboxgl.Marker()
        .setLngLat([friendCity.long, friendCity.lat])
        .setPopup(popup)
        .addTo(map);
    });
  },
  created: function() {
    axios.get("/api/map_connections").then((response) => {
      this.friendCities = response.data;
      console.log(response.data);
    });
  },
  methods: {},
};
</script>
