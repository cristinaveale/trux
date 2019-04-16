<template>
  <div>
    <!-- looping needs a unique key, hence the v-bind:key (must be a unique value) -->
    <div v-bind:key="truck.id" v-for="truck in trucks">
      <TruckItem v-bind:truck="truck" v-on:del-truck="$emit('del-truck',truck.id)"/>
    </div>
  </div>
</template>

<script>
import TruckItem from "./TruckItem";

export default {
  name: "Trucks",
  components: {
    TruckItem
  },
  props: ["trucks"]
};
</script>

<style scoped>
</style>
