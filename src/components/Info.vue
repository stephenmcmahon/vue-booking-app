<script setup>
  import { ref } from 'vue'
  const infoSubmitted = ref(false)
  const formData = ref({ 
    name: '', 
    email: '',
    phone: ''
  })
  const emits = defineEmits(['formSubmitted'])
  const handleSubmit = () => {
    const fieldName = document.forms['infoForm']['name'].value
    const fieldEmail = document.forms['infoForm']['email'].value
    const fieldPhone = document.forms['infoForm']['phone'].value
    if (fieldName == '' || fieldName == null) {
      alert('Name must be filled out')
      return false
    }
    if (fieldEmail == '' || fieldEmail == null) {
      alert('Email must be filled out')
      return false
    }
    if (fieldPhone == '' || fieldPhone == null) {
      alert('Phone must be filled out')
      return false
    }
    emits('formSubmitted', formData.value)
    const el = document.getElementById('submitBtn')
    if (el) {
      setTimeout(() => {
          el.style.display = 'none'
      }, 200)
    }
    infoSubmitted.value = true
  }
</script>

<template>
  <div>
    <span v-if="infoSubmitted">Info is still editable</span>
    <form name="infoForm" @submit.prevent="handleSubmit">
      <label for="name">Name:</label>
      <input class="infoField" type="text" id="name" name="name" v-model="formData.name" />
      <label for="email">Email:</label>
      <input class="infoField" type="email" id="email" name="email" v-model="formData.email" />
      <label for="phone">Phone:</label>
      <input class="infoField" type="tel" id="phone" name="phone" v-model="formData.phone" />
      <button type="submit" id="submitBtn">Submit</button>
    </form>
  </div>
</template>

<style scoped lang="scss">
  div {
    padding: 0 100px;
    @media only screen and (max-width: 600px) {
      padding: 0;
    }
    form {
      label {
        font-size: 12px;
        font-weight: bold;
        text-transform: uppercase;
        &::after{
          content: "\a";
          white-space: pre;
        }
      }
      input {
        width: 100%;
        height: 40px;
        margin: 3px 0 25px 0;
        padding: 0 10px;
      }
    }
  }
</style>
