<script setup lang="ts">
import {computed} from "vue";

const {todos, title} = defineProps<{ todos: Todo[], title: string }>()

import type {Todo} from "../App.vue";
import TodoItem from "./TodoItem.vue";

const tasksCount = computed(() => todos.length)

</script>

<template>
  <div class="todo-tasks-container" v-if="tasksCount">
    <p>{{ title }} - {{ tasksCount }}</p>
    <TodoItem
      v-for="todo in todos"
      :todo="todo"
      :key="todo.id"
    />
  </div>
</template>

<style scoped>
  .todo-tasks-container {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }
</style>