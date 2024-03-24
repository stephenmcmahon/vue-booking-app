<script setup>
  import { ref } from 'vue'
  const date = ref()

  const emits = defineEmits(['dateSelected'])

  const setDate = (value) => {
    date.value = value
    emits('dateSelected', date)
  }
</script>

<template>
  <DatePicker 
    :model-value="date"
    @update:model-value="setDate"
    time-picker-inline 
    :start-time="{ hours: 9, minutes: 0 }"
    :min-time="{ hours: 9, minutes: 0 }"
    :max-time="{ hours: 17, minutes: 0 }"
    minutes-increment="15"
    minutes-grid-increment="15"
    month-name-format="long"
    placeholder="Select Date"
  >
  </DatePicker>
</template>

<style scoped>

</style>