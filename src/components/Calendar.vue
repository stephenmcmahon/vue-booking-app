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
  <div id="datePicker">
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
  </div>
</template>

<style scoped lang="scss">
  #datePicker {
    background-color: var(--vt-c-text-dark-2);
    padding: 10px 100px;
    margin-bottom: 25px;
    border: 3px solid #04AA6D;
  }
</style>