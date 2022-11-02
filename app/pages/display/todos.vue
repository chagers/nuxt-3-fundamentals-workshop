<script setup>

const todoList = ref([]);

const route = useRoute();

const filteredTodoList = computed(() => {
  if (route.query.completed) {
    return completedItems.value;
  } else {
    return remainingItems.value;
  }
});

const completedItems = computed(() => {
  return todoList.value.filter(item => item.completed)
});

const remainingItems = computed(() => {
  return todoList.value.filter(item => !item.completed)
});
</script>

<template>
  <BaseDisplay title="ToDo Viewer" v-model:itemList="todoList">
    <template v-slot:hero>
      <img src="/todo.jpg" alt="Todo list" >
    </template>
    <template v-slot:items>
      <li v-for="todo in filteredTodoList" :key="`todo-id-${todo.id}`">
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
