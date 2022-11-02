<script setup>
import { defineEmits, defineProps, ref } from 'vue';

// Declaring this a var gives you access to 'props' object
// default array must be a func that generates a new array
const props = defineProps({
  itemList: {
    type: Array,
    default: () => [],
  },
  itemType: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
});

const emit = defineEmits(['update:itemList']);


function fetchItemList() {
  fetch(`https://jsonplaceholder.typicode.com/${props.itemType}`)
    .then(response => response.json())
    .then(json => {
      emit('update:itemList', json);
    })
}
</script>

<template>
  <div class="section">
    <slot name="hero" />
    <h1 class="title">{{ title }}</h1>
    <!-- By adding an emit to this event, the child can now bubble up
          data changes to the parent component,
          and leave any sort of computing at the parent level -->
    <button @click="fetchItemList">Fetch Data</button>
    <slot name="metrics" />
    <ul class="list">
      <slot name="items" :itemList="itemList" />
    </ul>
  </div>
</template>