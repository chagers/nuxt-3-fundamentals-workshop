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

// this is the baseline method upon which future methods are being developed
useAsyncData(`${itemType}Query`, () => {
  $fetch(`https://jsonplaceholder.typicode.com/${itemType}`)
    .then(response => {
      emit('update:itemList', response);
    })
});



// useLazyFetch(`https://jsonplaceholder.typicode.com/${itemType}`,
// response => {
//   emit('update:itemList', response)
// });



// const { data, pending, error, refresh } = await useFetch(`https://jsonplaceholder.typicode.com/${itemType}`, {
//   onRequest({ request, options }) {
//     // Set the request headers
//     options.headers = options.headers || {}
//     options.headers.authorization = '...'
//   },
//   onRequestError({ request, options, error }) {
//     // Handle the request errors
//   },
//   onResponse({ request, response, options }) {
//     // Process the response data
//     return response._data
//   },
//   onResponseError({ request, response, options }) {
//     // Handle the response errors
//   }
// });

// emit('update:itemList', data.value);

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