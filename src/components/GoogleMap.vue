<template>
  <div class="g-map"></div>
</template>

<script>
import gmapsInit from "../utils/gmaps";

export default {
  name: "gmap",
  async mounted() {
    try {
      const google = await gmapsInit();
      const geocoder = new google.maps.Geocoder();
      const map = new google.maps.Map(this.$el);

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
        }
        // ...
      ];

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

      const markers = locations.map(x => new google.maps.Marker({ ...x, map }));
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
