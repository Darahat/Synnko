<!-- ClearButton.vue -->
<template>
  <!-- Button to clear input -->
  <v-btn @click= "clearInputHandle">Clear Input</v-btn>
</template>

<script setup>
import {  ref } from 'vue';
const doClearFieldButtonClicked = ref(false);
// Define a function to emit a custom event
const clearInputHandle = () => {
  doClearFieldButtonClicked.value = true;
  emit('clearFieldButtonClick',doClearFieldButtonClicked.value)
}
const emit = defineEmits(['clearFieldButtonClick']);


</script>
