<template>
  <v-btn  @click= "handleButtonClick">Submit</v-btn>
</template>

<script setup>
import { defineComponent, ref,defineEmits } from 'vue';

// Define a function to emit a custom event
const buttonClicked = ref(false);
const handleButtonClick = () => {
  buttonClicked.value = true;
  emit('submitButtonClicked', buttonClicked.value) // Set buttonClicked to true when the button is clicked
    };
    const emit = defineEmits(['submitButtonClicked']);

</script>
