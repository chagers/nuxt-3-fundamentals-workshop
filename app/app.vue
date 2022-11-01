<script>
import { defineNuxtComponent } from '#app';

export default defineNuxtComponent({
  data: () => ({
    photoList: [],
  }),
  computed: {
    numberOfPhotos() {
      return this.photoList.length;
    },
    evenAlbums() {
      return this.photoList.filter(item => item.albumId % 2 === 0);
    },
    oddAlbums() {
      return this.photoList.filter(item => item.albumId % 2 !== 0);
    },
    evenAlbumPercentage() {
      return (this.evenAlbums.length / this.numberOfPhotos) || 0;
    },
  },
  methods: {
    fetchPhotoList() {
      fetch('https://jsonplaceholder.typicode.com/photos')
      .then(response => response.json())
      .then(json => {
        this.photoList = json;
      })
    },
  },
})
</script>

<template>
  <h1>Photo Gallery</h1>
  <button @click="fetchPhotoList">Fetch</button>
  <p>{{ numberOfPhotos }} total photos</p>
  <p>{{ evenAlbums.length }} total even photos</p>
  <p>{{ oddAlbums.length }} total odd photos</p>
  <p>{{ evenAlbumPercentage }} percentage of even photos</p>
  <ul>
    <li v-for="photo in photoList" :key="`photo-id-${photo.id}`">
      <img :src="photo.thumbnailUrl" :alt="photo.id">
    </li>
  </ul>
</template>

<style></style>
