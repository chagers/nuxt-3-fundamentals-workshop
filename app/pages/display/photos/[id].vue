<script setup>
const route = useRoute();
</script>

<template>
  <div>
    <h2 class="title">This is the album id: {{ route.params }}</h2>
  </div>
</template>

<style lang="scss" scoped>

</style>