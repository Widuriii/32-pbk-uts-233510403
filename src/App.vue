<script setup>
import { ref } from 'vue'

const tasks = ref([
  { id: 1, text: 'UTS PBK', done: false },
  { id: 2, text: 'Belajar Mandiri PBK', done: false }
])


</script>

<template>
  <header class="app-header">
    <h1 class="header">WeToDoList.com</h1>
  </header>

<div class="app">
<h1>What To Do List : </h1>
  <ul class="task-list">
    <li v-for="task in tasks" :key="task.id" class="task">
      <span>{{ task.text }}</span>
    </li>
  </ul>
</div>

  <footer>
    <p>Widuri-233510403</p>
    <p>Pemrograman Berbasis Komponen</p>
  </footer>
</template>

<style scoped>
</style>