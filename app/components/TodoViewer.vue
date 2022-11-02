<script setup>

import { defineProps, computed, ref } from 'vue';

  defineProps({
    title: {
      type: String,
      default: 'Hello Frontend Masters',
    }
  });

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
  <div class="section">
    
    <slot name="hero" />

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
    <h1 class="title">{{ title }}</h1>
    <button @click="fetchTodoList">Fetch Data</button>
    <!-- <slot name="metrics" :completed="completedItems" :remaining="remainingItems" /> -->
    <!-- You can also define default slot values, that will be overriden in parent, if defined there -->
    <slot name="metrics" :completed="completedItems" :remaining="remainingItems" >
      <p>
        {{ completedItems.length }} completed |
        {{ remainingItems.length }} remaining
      </p>
    </slot>
    <ul class="list">
      <li v-for="todo in todoList" :key="`todo-id-${todo.id}`">
        <input type="checkbox" :checked="todo.completed" /> {{ todo.title }}
      </li>
    </ul>
  </div>
</template>

<style lang="scss">
@import './node_modules/bulma/bulma.sass';
@import './assets/styles/main.scss';

:root {
  --text-color: #{$text-color};
}

.list {
  color: var(--text-color);
  display: grid;
  grid-template-columns: repeat(2, 1fr);
}
</style>
