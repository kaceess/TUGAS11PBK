<template>
    <p>Todo id: {{ todoId }}</p>
    <button class="btn btn-success" @click="fetchNextTodo" :disabled="!todoData">Fetch next todo</button>
    <p v-if="!todoData">Loading...</p>
    <pre v-else>{{ todoData }}</pre>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue'
  
  const todoId = ref(1)
  const todoData = ref(null)
  
  async function fetchData() {
    todoData.value = null
    const res = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
    )
    todoData.value = await res.json()
  }
  
  fetchData()
  
  const fetchNextTodo = () => {
    todoId.value++
  }
  
  watch(todoId, fetchData)
  </script>
  <style>
  @import url('https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css');
  @import url('https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css');
  </style>