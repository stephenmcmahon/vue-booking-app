<script setup>
  import VueCal from 'vue-cal'
</script>

<template>
  <vue-cal
    hide-view-selector
    :time="false"
    active-view="month"
    xsmall>
    <template #arrow-prev>
      <i class="icon material-icons">arrow_back</i>
    </template>
    <template #arrow-next>
      <i class="icon material-icons">arrow_forward</i>
    </template>
  </vue-cal>
</template>

<style scoped lang="scss">

</style>
