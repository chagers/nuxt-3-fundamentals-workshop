<script setup>
import { computed, ref } from 'vue';
import BaseDisplay from './BaseDisplay.vue';

let photoGallery = ref([])

const numberOfPhotos = computed(() => {
  return photoGallery.value.length
})

const evenAlbums = computed(() => {
  return photoGallery.value.filter(item => item.albumId % 2 === 0)
})

const oddAlbums = computed(() => {
  return photoGallery.value.filter(item => !(item.albumId % 2 === 0))
})

</script>

<template>
  <BaseDisplay title="Photo Gallery" itemType="photos" v-model:itemList="photoGallery">
    <template v-slot:items>
      <li v-for="photo in photoGallery" :key="`photo-id-${photo.id}`">
        <img :src="photo.thumbnailUrl" />
      </li>
    </template>
    <template v-slot:metrics>
      <p>
        {{ numberOfPhotos }} total ||
        {{ evenAlbums.length }} even |
        {{ oddAlbums.length }} odd
      </p>
    </template>
  </BaseDisplay>
</template>

<style lang="scss">
.photo-gallery-list {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
</style>
