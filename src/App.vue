<template>
  <div id="app">
    <!-- v-bind is a vue directive -->
    <Header/>
    <AddTruck v-on:add-truck="addTruck"/>
    <Trucks v-bind:trucks="trucks" v-on:del-truck="deleteTruck"/>
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Trucks from "./components/Trucks";
import AddTruck from "./components/AddTruck";
import axios from "axios";

export default {
  name: "app",
  components: {
    Header,
    Trucks,
    AddTruck
  },
  // Data is a function that returns an object
  data() {
    return {
      trucks: []
    };
  },
  methods: {
    deleteTruck(id) {
      this.trucks = this.trucks.filter(truck => truck.id !== id);
    },
    addTruck(newTruck) {
      this.trucks = [...this.trucks, newTruck];
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => (this.trucks = res.data))
      .catch(err => console.log("ERROR:", err));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #12800d;
  color: #fff;
  cursor: pointer;
}

.btn:hover {
  background: #12910d;
}
</style>
