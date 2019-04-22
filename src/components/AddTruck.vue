<template>
  <div>
    <!-- @submit calling the addTruck method-->
    <form @submit="addTruck">
      <input type="text" v-model="title" name="title" placeholder="Add a Food Truck">
      <input type="submit" value="Submit" class="btn">
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTruck",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    // As we add a truck, it will always be listed
    // inactive. uuid is a npm package that generates
    // a unique id - we will refactor once Cassandra/DSE
    // is implemented.
    addTruck(e) {
      e.preventDefault();
      const newTruck = {
        title: this.title,
        active: false
      };
      // send up to parent
      this.$emit("add-truck", newTruck);
      this.title = "";
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}

input[type="text"] {
  flex: 10;
  padding: 5px;
}

input[type="submit"] {
  flex: 2;
}
</style>
