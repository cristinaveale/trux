<template>
  <v-toolbar absolute color="teal lighten-3" dark>
    <v-toolbar-side-icon></v-toolbar-side-icon>

    <v-toolbar-title>Trux</v-toolbar-title>

    <v-spacer></v-spacer>

    <v-text-field
      hide-details
      prepend-icon="search"
      single-line
      placeholder="Search for your favorite food truck"
    ></v-text-field>

    <v-btn icon>
      <v-icon>my_location</v-icon>
    </v-btn>

    <v-btn icon>
      <v-icon>more_vert</v-icon>
    </v-btn>

    <v-btn icon>
      <v-icon>favorite</v-icon>
    </v-btn>

    <v-btn icon>
      <v-icon>more_vert</v-icon>
    </v-btn>
  </v-toolbar>
</template>

<script>
export default {
  name: "toolbar"
};
</script>

<style scoped>
</style>
