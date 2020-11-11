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
      friendCities: [
        {
          long: -122.4194,
          lat: 37.7749,
          description: "San Francisco",
        },
      ],
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
      var popup = new mapboxgl.Popup({ offset: 25 }).setText(
        friendCity.description
      );
      var marker = new mapboxgl.Marker()
        .setLngLat([friendCity.long, friendCity.lat])
        .setPopup(popup)
        .addTo(map);
    });
  },
  methods: {},
};
</script>
