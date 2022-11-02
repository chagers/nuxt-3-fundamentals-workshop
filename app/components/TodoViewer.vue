<script setup>
import { ref, computed } from 'vue';
import BaseDisplay from './BaseDisplay.vue';

const todoList = ref([]);

const completedItems = computed(() => {
  return todoList.value.filter(item => item.completed)
});

const remainingItems = computed(() => {
  return todoList.value.filter(item => !item.completed)
});
</script>

<template>
  <BaseDisplay title="ToDo Viewer" itemType="todos" v-model:itemList="todoList">
    <template v-slot:hero>
      <img src="/todo.jpg" alt="Todo list" >
    </template>
    <template v-slot:items>
      <li v-for="todo in todoList" :key="`todo-id-${todo.id}`">
        <input type="checkbox" :checked="todo.completed" /> {{ todo.title }}
      </li>
    </template>
    <template v-slot:metrics>
      <p>
        {{ completedItems.length }} completed |
        {{ remainingItems.length }} remaining
      </p>
    </template>
  </BaseDisplay>
</template>

<style lang="scss"></style>
