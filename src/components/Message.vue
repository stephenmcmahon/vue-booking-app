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
      <textarea class="infoField" id="message" name="message" v-model="message" placeholder="Enter Message Here..." maxlength ="1000"></textarea>
      <button type="submit">Submit Message</button>
    </form>
  </div>
</template>

<style scoped lang="scss">
  div {
    form {
      text-align: center;
      textarea {
        width: 100%;
        height: 125px;
        padding: 5px;
        resize: none;
      }
      button {
        background-color: #04AA6D;
      }
    }
  }
</style>
