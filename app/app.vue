<script setup>

import PhotoGallery from './components/PhotoGallery.vue';
import TodoViewer from './components/TodoViewer.vue';

</script>

<template>
  <div class="container">
    <div class="section">
      <div class="columns">
        <div class="column">
          <PhotoGallery />
        </div>
        <div class="column">
          <TodoViewer title="this is my todo viewer">
            <!-- <template v-slot:hero> -->
            <template #hero>
              <h2 class="">This is a slot</h2>
            </template>
            <!-- <template #metrics="slotProps"> -->
              <!-- Can destructure props, but keep in mind it will refer to all passed props -->
            <template #metrics="{ completed, remaining }">
              <!-- Slot Props should be used for display purposes only
                    do not use for managing state between parent and child -->
              <strong>Completed: {{ completed.length }}</strong>
              <strong>Remaining: {{ remaining.length }}</strong>
              <h3 class="">this is the metrics slot</h3>
              <pre>{{ completed }}</pre>
            </template>
          </TodoViewer>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
