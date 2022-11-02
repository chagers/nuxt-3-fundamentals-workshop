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
  <NuxtLayout name="todo">
    <div class="section">
      <h1 class="title">Todo Viewer</h1>
      <NuxtPage v-if="route.params.id" />
      <BaseDisplay v-else title="ToDo Viewer" v-model:itemList="todoList">
        <template v-slot:hero>
          <img src="/todo.jpg" alt="Todo list" >
        </template>
        <template v-slot:items>
          <li v-for="todo in filteredTodoList" :key="`todo-id-${todo.id}`">
            <input type="checkbox" :checked="todo.completed" />
            <NuxtLink :to="`/display/todos/${todo.id}`">{{ todo.title }}</NuxtLink>
          </li>
        </template>
        <template v-slot:metrics>
          <p>
            {{ completedItems.length }} completed |
            {{ remainingItems.length }} remaining
          </p>
        </template>
      </BaseDisplay>
      <!-- Display a child in a page w/out having the whole page refresh -->
    </div>
  </NuxtLayout>
</template>

<style lang="scss"></style>
