<template>
 <div>

  <v-text-field
v-model="formattedDate"

                @click = "showDatePicker"
                append-icon="mdi-calendar"
            ></v-text-field>
              <!-- {{ props.myvariable }} -->
            <v-dialog
      v-model="isVisible"
      width="auto"
    >


    <v-date-picker
v-model="selectedDate"

            v-click-outside="hideDatePIcker"
        >
         </v-date-picker>
    </v-dialog>

 </div>
</template>

<script setup>
import { ref, defineProps, watch, computed } from 'vue';

const props = defineProps({
  clearInputValue: Boolean,
  submitInputValue: Boolean,
});
// Watch for changes in clearInputValue prop

const selectedDate = ref(null);
const modifyDate = ref(null);
 const formattedDate = computed(() => {
  if (selectedDate.value) {
    const dateObj = new Date(selectedDate.value);
    const month = String(dateObj.getMonth() + 1).padStart(2, '0');
    const day = String(dateObj.getDate()).padStart(2, '0');
    const year = dateObj.getFullYear();
    // Formatting the date as "MM/DD/YYYY" for display
    modifyDate.value = `${year}-${month}-${day}`;
    return `${month}/${day}/${year}`;
  } else {
    return ''; // If no date is selected, return an empty string
  }
});
watch(() => props.clearInputValue, (newVal) => {
  if (newVal) {
    // Clear the selected date
    selectedDate.value = null;
  }
});
watch(() => props.submitInputValue, (newVal) => {
  if (newVal) {
     console.log(modifyDate.value);
  }
});

const isVisible = ref(false);
const showDatePicker = () => {
  console.log(isVisible);
  isVisible.value = true;
 }
const hideDatePIcker = () => {
  isVisible.value = false;
 }
</script>
