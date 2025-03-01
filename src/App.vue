<script setup>
import { ref } from "vue";

const msg = ref("Shopping List");
const items = ref([
  { id: 1, label: "10 party hats" },
  { id: 2, label: "2 board games" },
  { id: 3, label: "20 cups" },
]);
</script>

<template>
  <h1>{{ msg }}</h1>
  <ul v-for="item in items" :key="item.id">
    {{
      item.label
    }}
  </ul>
</template>
