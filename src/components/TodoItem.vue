<script setup lang="ts">
import CheckIcon from '../assets/check-icon.svg'
import TrashIcon from '../assets/trash-icon.svg'
import CrossIcon from '../assets/cross-icon.svg'
import type {Todo} from "../App.vue";
import {inject} from "vue";

const { todo } = defineProps<{ todo: Todo }>()

const removeTask = inject<(taskId: number) => void>('removeTask')
const toggleCompleteTask = inject<(taskId: number) => void>('toggleCompleteTask')

</script>

<template>
  <div class="todo-item-container" :data-completed="todo.completed">
    <p class="text">{{ todo.text }}</p>
    <div class="buttons">
      <CrossIcon v-if="todo.completed" @click="toggleCompleteTask?.(todo.id)" />
      <CheckIcon v-else @click="toggleCompleteTask?.(todo.id)" />
      <TrashIcon  @click="removeTask?.(todo.id)" />
    </div>
  </div>
</template>

<style scoped>
  .todo-item-container {
    display: flex;
    background-color: #15101C;
    border-radius: 10px;
    padding: 25px 20px;
    color: #9E78CF;
    gap: 24px
  }

  .todo-item-container[data-completed="true"] {
    color: #78CFB0;
    text-decoration: line-through;
  }

  .text {
    width: 100%;
    word-break: break-word;
    overflow-wrap: break-word;
    white-space: normal;
  }

  .buttons {
    display: flex;
    gap: 16px;
  }

  .buttons > *:hover {
    opacity: .5;
    cursor: pointer;
  }
</style>