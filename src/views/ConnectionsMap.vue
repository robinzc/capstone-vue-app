<template>
  <div class="connections-map">
    <h1>{{ message }}</h1>
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
import mapboxgl from "mapbox-gl";
export default {
  data: function() {
    return {
      message: "Your Travel Universe",
    };
  },
  mounted: function() {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_ACCESS_TOKEN;
    const map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
      center: [-122.431297, 37.773972], // starting position [lng, lat]
      zoom: 10, // starting zoom
    });
  },
  methods: {},
};
</script>
