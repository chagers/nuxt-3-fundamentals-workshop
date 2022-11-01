<script setup>
// 'setup' indicates composition api is being used

import { computed, ref, reactive } from 'vue'

let photoGallery = ref([])

// let photoGallery = ref({
//   id: 234,
//   title: 'Best Photo Ever 2'
// })
// this is more declarative that you're using a reactive reference
// how to get values using 'ref':
// photoGallery.value.title

// let newPhoto = reactive({
//   id: 123,
//   title: 'Best Photo Ever'
// })
// obfuscates that you're using a reactive reference, but syntax is shorter
// how to get values using 'reactive':
// newPhoto.title

const numberOfPhotos = computed(() => {
  return photoGallery.value.length
})

const evenAlbums = computed(() => {
  return photoGallery.value.filter(item => item.albumId % 2 === 0)
})

const oddAlbums = computed(() => {
  return photoGallery.value.filter(item => !(item.albumId % 2 === 0))
})

// can use this syntax, or arrow syntax - no preference
// Ben likes using 'function' syntax, because it gives a nice visual
// distinction between computed vars and methods
function fetchPhotoGallery() {
  fetch('https://jsonplaceholder.typicode.com/photos')
    .then(response => response.json())
    .then(json => {
      photoGallery.value = json
    })
}
</script>

<template>
  <h1>Photo Gallery</h1>
  <button @click="fetchPhotoGallery">Fetch Data</button>
  <p>
    {{ numberOfPhotos }} photos ({{ oddAlbums.length }} odd albums |
    {{ evenAlbums.length }} even albums)
  </p>
  <ul>
    <li v-for="photo in photoGallery" :key="`photo-id-${photo.id}`">
      <img :src="photo.thumbnailUrl" />
    </li>
  </ul>
</template>

<style></style>
