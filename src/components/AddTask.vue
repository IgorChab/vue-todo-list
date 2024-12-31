<script setup lang="ts">
const emit = defineEmits<{
 addTask: [text: string]
}>()

import AddIcon from '../assets/add-icon.svg'
import {ref} from "vue";

const text = ref('')

const createTodo = () => {
  if (text.value) {
    emit('addTask', text.value)
    text.value = ''
  }
}
</script>

<template>
  <div class="add-task-container">
    <input type="text" placeholder="Add a new task" class="input" v-model.trim="text" @keyup.enter="createTodo" />
    <button type="submit" class="button" @click="createTodo" :disabled="!text">
      <AddIcon />
    </button>
  </div>
</template>

<style scoped>
  .add-task-container {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .input {
    width: 100%;
    height: 40px;
    border: 1px solid #3E1671;
    padding: 0 16px;
    border-radius: 10px;
    background-color: transparent;
    outline: none;
    color: #777777;
    font-size: 16px;
  }

  .button {
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #9E78CF;
    border: none;
    outline: none;
    border-radius: 10px;
    transition: .3s;
    flex-shrink: 0;
  }

  .button:disabled {
    opacity: .5;
  }
</style>