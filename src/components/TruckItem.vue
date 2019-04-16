<template>
  <div class="truck-item" v-bind:class="{'not-active':!truck.active}">
    <p>
      <input type="checkbox" v-on:change="markInactive">
      {{truck.title}}
    </p>
    <button class="del" @click="$emit('del-truck',truck.id)">Delete</button>
  </div>
</template>

<script>
export default {
  name: "TruckItem",
  props: ["truck"],
  methods: {
    markInactive() {
      this.truck.active = !this.truck.active;
    }
  }
};
</script>

<style scoped>
.truck-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px dotted;
  display: flex;
  align-items: baseline;
  justify-content: space-between;
}

.not-active:after {
  content: "inactive";
  border: 1px solid black;
  padding: 4px;
  background: #1c1e27;
  color: white;
  font-size: 12px;
}

.del {
  background: #5e0317;
  color: #fff;
  border: none;
  border-radius: 2px;
  padding: 5px 9px;
  cursor: pointer;
  order: 3;
  box-shadow: 1px 1px 2px #333;
}
</style>
