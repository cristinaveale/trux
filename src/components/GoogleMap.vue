<template>
  <div class="g-map"></div>
</template>

<script>
import MarkerClusterer from "@google/markerclusterer";
import gmapsInit from "../utils/gmaps";

export default {
  name: "gmap",
  async mounted() {
    try {
      const google = await gmapsInit();
      const geocoder = new google.maps.Geocoder();
      const map = new google.maps.Map(this.$el);

      // Setting dummy food truck locations
      const locations = [
        {
          position: {
            lat: 47.65082,
            lng: -122.37643
          }
        },
        {
          position: {
            lat: 47.60046,
            lng: -122.33247
          }
        },
        {
          position: {
            lat: 47.61966,
            lng: -122.3385
          }
        }
      ];

      // Applying this map to Seattle, WA
      geocoder.geocode({ address: "Seattle, WA" }, (results, status) => {
        if (status !== "OK" || !results[0]) {
          throw new Error(status);
        }
        map.setCenter(results[0].geometry.location);
        map.fitBounds(results[0].geometry.viewport);
      });

      // When cluster is clicked, map will zoom in to cluster position
      const markers = locations.map(location => {
        const marker = new google.maps.Marker({ ...location, map });
        marker.addListener("click", () => markerClickHandler(marker));
        return marker;
      });

      // Adding event listener to single marker, once clicked,
      // map will move to that single location
      const markerClickHandler = marker => {
        map.setZoom(17);
        map.setCenter(marker.getPosition());
      };

      // Image of bundled cluster
      new MarkerClusterer(map, markers, {
        imagePath:
          "https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m"
      });
    } catch (error) {
      console.error(error);
    }
  }
};
</script>

<style>
.g-map {
  width: 100vw;
  height: 500px;
}
</style>
