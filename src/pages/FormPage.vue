<template>
  <v-card class="mx-auto my-8" elevation="16" max-width="345">
    <v-card-item>
      <v-card-title>
        Synnko's Cost Form
      </v-card-title>
    </v-card-item>

    <v-card-text>
      <ClearButton @clearFieldButtonClick="clearInput" />
      <ConstField v-model="numberValue" :submitInputValue=submitInputValue :clearInputValue=clearInputValue />
      <DatePicker :submitInputValue=submitInputValue :clearInputValue=clearInputValue />
      <submitButton @submitButtonClicked="SubmitInput" />
    </v-card-text>
  </v-card>
</template>

<script setup>
import { ref } from 'vue';

import DatePicker from '../components/DatePicker.vue';
const inputValue = ref('Not Clear');
const numberValue = ref('');
const clearInputValue = ref(false);
const submitInputValue = ref(false);
const SubmitInput = (value) => {
  submitInputValue.value = value;
}

const clearInput = (value) => {
  clearInputValue.value = value;
};

</script>
