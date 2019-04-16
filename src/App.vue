<template>
  <div id="app">
    <!-- v-bind is a vue directive -->
    <Header/>
    <AddTruck/>
    <Trucks v-bind:trucks="trucks" v-on:del-truck="deleteTruck"/>
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Trucks from "./components/Trucks";
import AddTruck from "./components/AddTruck";

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
      trucks: [
        {
          id: 1,
          title: "All Star Cafe",
          twitterUrl: "https://twitter.com/ASCafeMobile/",
          active: true
        },
        {
          id: 2,
          title: "The Dumpling Lady",
          twitterUrl: "https://twitter.com/DumplingLadyCLT",
          active: true
        },
        {
          id: 3,
          title: "Hiya Food Truck",
          twitterUrl: "https://twitter.com/hiyafoodtruck",
          active: true
        }
      ]
    };
  },
  methods: {
    deleteTruck(id) {
      this.trucks = this.trucks.filter(truck => truck.id !== id);
    }
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
