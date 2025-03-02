<script setup>
import { ref } from "vue";

// Reactive reference for the list header
const header = ref("Shopping List");
const editing = ref(false);

// Array holding shopping list items, each item has an id and label
const items = ref([
  // { id: 1, label: "10 party hats" },
  // { id: 2, label: "2 board games" },
  // { id: 3, label: "20 cups" },
]);

// Ref for new item input
const newItem = ref("");

// Boolean ref to mark high-priority items (currently not used)
const highPriority = ref(false);

// Function to add new items to the list
const saveItems = () => {
  // Prevent adding empty items
  // if (!newItem.value.trim()) return;

  // Add the new item to the list with a unique ID
  items.value.push({
    id: Date.now(), // Ensures a unique ID
    label: newItem.value,
  });

  // Clear input after adding
  newItem.value = "";
};
const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
};
</script>

<template>
  <!-- Page Header -->
  <div class="header">
    <h1>{{ header }}</h1>
    <button class="btn" @click="doEdit(false)">Cancel</button>
    <button class="btn btn-primary" @click="doEdit(true)">Add Items</button>
  </div>

  <!-- Form to Add New Items -->
  <form v-if="editing" class="add-item-form" @submit.prevent="saveItems">
    <!-- Input for new items -->
    <input type="text" v-model.trim="newItem" placeholder="add new items" />

    <!-- Checkbox for high priority (not currently used in logic) -->
    <label>
      <input type="checkbox" v-model="highPriority" value="high" />
      High Priority
    </label>

    <!-- Button to submit the new item -->
    <button class="btn btn-primary">Save Items</button>
  </form>

  <!-- List of Items -->
  <ul>
    <li v-for="({ id, label }, index) in items" :key="id">
      {{ label }}
    </li>
  </ul>
  <p v-if="!items.length">Nothing to show</p>
</template>
