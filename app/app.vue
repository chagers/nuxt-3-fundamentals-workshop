<script setup>
// Composition API is just vanilla JS

import { computed, ref } from 'vue';

  // if you defined this with 'let todoList = []', it'd
  // automagically make it reactive on compile.
  // defining with the helper method 'ref' makes
  // it clear that we're using vue's help here.
  const todoList = ref([]);

  const completedItems = computed(() => {
    return todoList.value.filter(item => item.completed);
  });

  const remainingItems = computed(() => {
    return todoList.value.filter(item => !item.completed);
  });

  const fetchTodoList = () => {
    fetch('https://jsonplaceholder.typicode.com/todos/')
      .then(response => response.json())
      .then(json => {
        todoList.value = json
      })
  };
</script>

<template>
  <!-- Note: NUXT requires a single root in templates (Vue 3 does not)
        This helps NUXT determine what to hydrate, how to contain 
        elements for page transitions, etc. -->
  <div>
    <img src="/todo.jpg" alt="Todo photo by Glenn Casterns-Peters" />
    <p>
      Photo by
      <a
        href="https://unsplash.com/@glenncarstenspeters?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText"
        >Glenn Carstens-Peters</a
      >
      on
      <a
        href="https://unsplash.com/s/photos/todo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText"
        >Unsplash</a
      >
    </p>
    <h1>Hello Frontend Masters!</h1>
    <button @click="fetchTodoList">Fetch Data</button>
    <p>
      {{ completedItems.length }} completed |
      {{ remainingItems.length }} remaining
    </p>
    <ul>
      <li v-for="todo in todoList" :key="`todo-id-${todo.id}`">
        <input type="checkbox" :checked="todo.completed" /> {{ todo.title }}
      </li>
    </ul>
  </div>
</template>
