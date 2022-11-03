<script setup></script>

<template>
  <NuxtLayout name="display">
    <div class="container">
      <div class="section">
        <h1 class="title">Display</h1>
        <NuxtPage />
      </div>
    </div>
  </NuxtLayout>
</template>

<style lang="scss">
.photo-gallery-list {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
</style>
