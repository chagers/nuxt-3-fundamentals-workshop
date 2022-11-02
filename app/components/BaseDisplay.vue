<script setup>

const route = useRoute();

// get the item type from the url params
const itemType = route.path.split('/')[2];

const props = defineProps({
  itemList: {
    type: Array,
    default: () => [],
  },
  title: {
    type: String,
    required: true,
  },
});

const emit = defineEmits(['update:itemList']);

// immediately fetch your data on page load
// see lifecycle methods for more details
fetch(`https://jsonplaceholder.typicode.com/${itemType}`)
  .then(response => response.json())
  .then(json => {
    emit('update:itemList', json);
  })
</script>

<template>
  <div class="section">
    <slot name="hero" />
    <h1 class="title">{{ title }}</h1>
    <slot name="metrics" />
    <ul class="list">
      <slot name="items" :itemList="itemList" />
    </ul>
  </div>
</template>