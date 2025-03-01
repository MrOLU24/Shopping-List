<script setup>
import { ref } from "vue";

const header = ref("Shopping List");
const items = ref([
  { id: 1, label: "10 party hats" },
  { id: 2, label: "2 board games" },
  { id: 3, label: "20 cups" },
]);
const priority = ref("high");

</script>

<template>
  <h1>{{ header }}</h1>
  <input type="text" />
  <button>Add</button>
<label for="priority">
  High:
  <input v-model="priority" type="radio">
</label>
<label for="">
  Low:
  <input v-model="priority" type="radio">
</label>

  <ul v-for="({id, label}, index) in items" :key="id">
    <li>{{ label }}</li>
  </ul>
</template>
