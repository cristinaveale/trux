<template>
  <div>
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
