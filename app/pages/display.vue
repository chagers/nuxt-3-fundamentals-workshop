<script setup></script>

<template>
  <div class="container">
    <div class="section">
      <h1 class="title">Display</h1>
      <!-- Adding a key attribute forces refresh -->
      <!-- Pulls in pages listed in display folder,
            and means that only those pages are loaded
            when their nested route is hit -->
      <NuxtPage />
    </div>
  </div>
</template>

<style lang="scss">
.photo-gallery-list {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
</style>
