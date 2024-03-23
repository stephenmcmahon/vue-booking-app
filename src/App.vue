<script setup>
  import Info from './components/Info.vue'
  import Calendar from './components/Calendar.vue'
  import Message from './components/Message.vue'
  import { ref } from 'vue'

  const infoSubmitted = ref(false)
  const dateSubmitted = ref(false)
  const infoConfirmed = ref(false)

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

  const handleConfirm = () => {
    infoConfirmed.value = true
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
      <button @click="handleConfirm">Confirm Info and Date</button>
    </div>
    <div v-if="infoConfirmed">
      <Message />
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
