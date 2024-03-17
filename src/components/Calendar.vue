<script setup>
  import VueCal from 'vue-cal'
  import { ref } from 'vue'

  const selectedDate = new Date()

  // const events = ref([])
  // const options = {
  //   editable: true,
  //   draggable: true,
  //   resizable: true,
  //   defaultView: 'month',
  //   disableViews: ['years', 'year', 'week', 'day']
  // }

  // const newEvent = ref({
  //   title: '',
  //   start: '',
  //   end: ''
  // })

  // const addEvent = () => {
  //   events.value.push({
  //     title: newEvent.value.title,
  //     start: new Date(newEvent.value.start),
  //     end: new Date(newEvent.value.end)
  //   })
  //   newEvent.value = { title: '', start: '', end: '' }
  // }
</script>

<template>
  <div>
    <vue-cal
      xsmall
      hide-view-selector
      :time="false"
      :transitions="false"
      active-view="month"
      :disable-views="['week', 'day']"
      :selected-date="selectedDate"
      style="width: 210px; height: 230px">
      <template #arrow-prev>
        <i class="icon material-icons">arrow_back</i>
      </template>
      <template #arrow-next>
        <i class="icon material-icons">arrow_forward</i>
      </template>
    </vue-cal>
    <p>Selected date: '{{ selectedDate.format() }}'</p>
    <!-- <form @submit.prevent="addEvent">
      <label for="title">Title:</label>
      <input type="text" id="title" v-model="newEvent.title" required><br>
      <label for="start">Start Date:</label>
      <input type="datetime-local" id="start" v-model="newEvent.start" required><br>
      <label for="end">End Date:</label>
      <input type="datetime-local" id="end" v-model="newEvent.end" required><br>
      <button type="submit">Add Event</button>
    </form> -->
  </div>
</template>

<style scoped lang="scss">

</style>
