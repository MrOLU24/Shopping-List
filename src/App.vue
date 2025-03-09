<script setup>
import { computed, ref } from "vue";

// Reactive reference for the list header.

const header = ref("Shopping List");
const editing = ref(false);
const characterCount = computed(() => {
  return newItem.value.length;
});
const reverseitem = computed(()=>{
  return [...items.value].reverse()
})

// Array holding shopping list items, each item has an id and label.

const items = ref([
  { id: 1, label: "10 party hats", purchased: true, highPriority: false },
  { id: 2, label: "2 board games", purchased: true, highPriority: false },
  { id: 3, label: "20 cups", purchased: false, highPriority: true },
]);
// Ref for new item input
const newItem = ref("");
// Boolean ref to mark high-priority items (currently not used)
const newHighPriority = ref(false);

// Function to add new items to the list
const saveItems = () => {
  // Prevent adding empty items
  if (!newItem.value.trim()) return;

  // Add the new item to the list with a unique ID
  items.value.push({
    id: Date.now(), // Ensures a unique ID
    label: newItem.value,
    highPriority: newHighPriority.value,
  });

  // Clear input after adding
  newItem.value = "";
  newHighPriority.value = "";
};
const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
  newHighPriority;
};

const togglePurchased = (item) => {
  item.purchased = !item.purchased;
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
      <input type="checkbox" v-model="newHighPriority" value="high" />
      High Priority
    </label>

    <!-- Button to submit the new item -->
    <button class="btn btn-primary">Save Items</button>
  </form>
  <p>{{ characterCount }}/20</p>

  <!-- List of Items -->
  <ul>
    <li
      @click="togglePurchased(items)"
      v-for="(items, index) in reverseitem"
      :key="items.id"
      class="static-class"
      :class="{ strikeout: items.purchased, priority: items.highPriority }"
    >
      {{ items.label }}
    </li>
  </ul>
  <p v-if="!items.length">Nothing to show</p>
</template>
