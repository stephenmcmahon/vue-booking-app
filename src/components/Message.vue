<script setup>
  const handleSubmit = () => {
  }
</script>

<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <textarea name="message">Enter text here...</textarea>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<style scoped lang="scss">

</style>
