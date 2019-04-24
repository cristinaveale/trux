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
            lat: 35.226433,
            lng: -80.84285
          }
        },
        {
          position: {
            lat: 35.216108,
            lng: -80.82211
          }
        },
        {
          position: {
            lat: 35.283011,
            lng: -80.900585
          }
        }
      ];

      // Applying this map to Charlotte, NC
      geocoder.geocode(
        { address: "Charlotte, North Carolina" },
        (results, status) => {
          if (status !== "OK" || !results[0]) {
            throw new Error(status);
          }

          map.setCenter(results[0].geometry.location);
          map.fitBounds(results[0].geometry.viewport);
        }
      );

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
  height: 100vh;
}
</style>
