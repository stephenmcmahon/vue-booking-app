<script setup>
  import { ref } from 'vue'
  const message = ref()
  const emits = defineEmits(['messageSubmitted'])
  const handleSubmit = () => {
    emits('messageSubmitted', message)
  }
</script>

<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <textarea class="infoField" id="message" name="message" v-model="message" placeholder="Enter Message Here..."></textarea>
      <button type="submit">Submit Message</button>
    </form>
  </div>
</template>

<style scoped lang="scss">
  div {
    form {
      textarea {
        width: 100%;
        height: 75px;
      }
      button {
        background-color: #04AA6D;
      }
    }
  }
</style>
