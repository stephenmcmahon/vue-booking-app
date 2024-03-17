<script setup>
  import Info from './components/Info.vue'
  import Calendar from './components/Calendar.vue'
  import { ref } from 'vue'

  const infoSubmitted = ref(false)
  const infoData = ref({ 
    name: '', 
    email: '',
    phone: ''
  })

  const handleFormSubmitted = (data) => {
    infoData.value = data
    infoSubmitted.value = true
  }
</script>

<template>
  <div>
    <Info @formSubmitted="handleFormSubmitted" />
    <Calendar v-if="infoSubmitted" />
    <div v-if="infoSubmitted">
      <p>Name: {{ infoData.name }}</p>
      <p>Email: {{ infoData.email }}</p>
      <p>Phone: {{ infoData.phone }}</p>
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
