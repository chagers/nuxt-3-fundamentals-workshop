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
  <!-- Ensure single child in template -->
  <div class="section">
    <NuxtPage v-if="route.params.id" />
    <BaseDisplay v-else title="Photo Gallery" v-model:itemList="photoGallery">
      <template v-slot:items>
        <li v-for="photo in filteredPhotoGallery" :key="`photo-id-${photo.id}`">
          <NuxtLink :to="`/display/photos/${photo.id}`">
            <img :src="photo.thumbnailUrl" />
          </NuxtLink>
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
  </div>
</template>

<style lang="scss">
.photo-gallery-list {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
</style>
