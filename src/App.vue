<script setup>
  import Info from './components/Info.vue'
  import Calendar from './components/Calendar.vue'
  import { ref } from 'vue'

  const infoSubmitted = ref(false)
  const dateSubmitted = ref(false)

  const infoData = ref({ 
    name: '', 
    email: '',
    phone: ''
  })

  const dateData = ref({ 
    date: ''
  })

  const handleFormSubmitted = (data) => {
    infoData.value = data
    infoSubmitted.value = true
  }

  const handleDateSubmitted = (data) => {
    dateData.value = data
    dateSubmitted.value = true
  }

</script>

<template>
  <div>
    <Info @formSubmitted="handleFormSubmitted" />
    <div v-if="infoSubmitted">
      <Calendar @dateSelected="handleDateSubmitted" />
      <p>Name: {{ infoData.name }}</p>
      <p>Email: {{ infoData.email }}</p>
      <p>Phone: {{ infoData.phone }}</p>
    </div>
    <div v-if="dateSubmitted">
      <p>Date Selected: {{ dateData.value }}</p>

      <button>Confirm Info and Date</button>
    </div>
  </div>
</template>

<style scoped lang="scss">
  div {
    width: 600px;
    max-width: 600px;
    margin: auto;
  }
</style>
