<script setup lang="ts">
import AddTask from "./components/AddTask.vue";
import {computed, ref, provide, watch} from "vue";
import TaskList from "./components/TaskList.vue";

export interface Todo {
  id: number
  completed: boolean
  text: string
}

const persistedTodos = localStorage.getItem('todos')
const initialTodos = persistedTodos ? JSON.parse(persistedTodos) : []

const todos = ref<Todo[]>(initialTodos)

watch(todos, (value) => {
  localStorage.setItem('todos', JSON.stringify(value))
}, { deep: true })

const addTask = (text: string) => {
  todos.value.push({
    id: Date.now(),
    completed: false,
    text
  })
}

const removeTask = (taskId: number) => {
  todos.value = todos.value.filter((todo) => todo.id !== taskId)
}

const toggleCompleteTask = (taskId: number) => {
  todos.value = todos.value.map((todo) => {
    if (todo.id === taskId) {
      return {
        ...todo,
        completed: !todo.completed
      }
    }

    return todo
  })
}


provide('removeTask', removeTask)
provide('toggleCompleteTask', toggleCompleteTask)

const todoTasks = computed(() => {
  return todos.value.filter((todo) => !todo.completed)
})

const doneTasks = computed(() => {
  return todos.value.filter((todo) => todo.completed)
})

</script>

<template>
  <div class="container">
    <div class="wrapper">
      <AddTask @add-task="addTask" />
      <TaskList
        :todos="todoTasks"
        title="Tasks to do"
      />
      <TaskList
        :todos="doneTasks"
        title="Done"
      />
    </div>
  </div>
</template>

<style scoped>
  .container {
    display: flex;
    justify-content: center;
  }

  .wrapper {
    width: 30rem;
    padding: 10rem 0;
    display: flex;
    flex-direction: column;
    gap: 5rem;
  }
</style>
