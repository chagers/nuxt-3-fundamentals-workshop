<script setup>
const photoGallery = ref([]);

const route = useRoute();

const filteredPhotoGallery = computed(() => {
  if (route.query.even) {
    return evenAlbums.value.slice(0, 5);
  } else {
    return photoGallery.value.slice(0, 5);
  }
});

const numberOfPhotos = computed(() => {
  return photoGallery.value.length
})

const evenAlbums = computed(() => {
  return photoGallery.value.filter(item => item.albumId % 2 === 0)
});

const oddAlbums = computed(() => {
  return photoGallery.value.filter(item => !(item.albumId % 2 === 0))
});
</script>

<template>
  <BaseDisplay title="Photo Gallery" v-model:itemList="photoGallery">
    <template v-slot:items>
      <li v-for="photo in filteredPhotoGallery" :key="`photo-id-${photo.id}`">
        <span>{{ photo.id }}</span>
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
