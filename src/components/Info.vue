<script setup>
  import { ref, defineEmits } from 'vue'

  const formData = ref({ 
    name: '', 
    email: '' 
  })

  const emits = defineEmits(['formSubmitted'])

  const handleSubmit = () => {
    emits('formSubmitted', formData.value)
  }
</script>

<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="formData.name" />

      <label for="email">Email:</label>
      <input type="email" id="email" v-model="formData.email" />

      <label for="phone">Phone:</label>
      <input type="tel" id="phone" v-model="formData.phone" />

      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<style scoped lang="scss">

</style>
