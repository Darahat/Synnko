<template>
  <!-- Input field with Vue Material design and clearable functionality -->
<div>


  <v-text-field v-model="inputValue" clearable label="Enter a number" outlined type="text" @input="formatInput"
    :rules="inputRules" />
  </div>
</template>

<script setup>
import { defineProps, ref,watch } from 'vue';


    // Reference to store the input value
    const inputValue = ref('');
    const props = defineProps({
      clearInputValue: Boolean,
      submitInputValue: Boolean,
});
// Watch for changes in clearInputValue prop
watch(() => props.clearInputValue, (newVal) => {
  if (newVal) {
    // Clear the input field
    inputValue.value = '';
  }
});
watch(() => props.submitInputValue, (newVal) => {
  if (newVal) {

    console.log(inputValue.value);
  }
});
const value = ref('');



    // Function to format the input number with commas
    const formatNumber = (number) => {
      // Remove existing commas
      let numberString = number.replace(/,/g, '');
      // Separate integer and decimal parts
      let integerPart = '';
      let decimalPart = '';
      const decimalIndex = numberString.indexOf('.');
      if (decimalIndex !== -1) {
        integerPart = numberString.substring(0, decimalIndex);
        decimalPart = numberString.substring(decimalIndex);
      } else {
        integerPart = numberString;
      }

      // Format integer part with commas
      if (integerPart.length > 3) {
        const parts = [];
        let part = '';
        for (let i = integerPart.length - 1, count = 0; i >= 0; i--) {
          part = integerPart[i] + part;
          count++;
          if (count === 3 || i === 0) {
            parts.unshift(part);
            part = '';
            count = 0;
          }
        }
        integerPart = parts.join(',');
      }

      return integerPart + decimalPart;
    };

// Function to format the input value as the user types

const formatInput = (event) => {
  const input = event.target;
  const currentValue = input.value.replace(/,/g, ''); // Remove existing commas before formatting
  const formattedValue = formatNumber(currentValue);
  input.value = formattedValue;
  inputValue.value = formattedValue;
}

    // Validation rules for the input field
    const inputRules = [
      (value) => /^[0-9,]*(?:\.\d{0,2})?$/.test(value) || 'Invalid number format', // Adjusted for comma separator
    ];


</script>

<style scoped>
/* Optional styling for your component */
</style>
