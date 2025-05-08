<script setup>
import { ref, computed } from 'vue'

const tasks = ref([
  { id: 1, text: 'UTS PBK', done: false },
  { id: 2, text: 'Belajar Mandiri PBK', done: false }
])

const newTask = ref('')
const addTask = () => {
  if (!newTask.value.trim()) 
    return 
  tasks.value.push({
    id: Date.now(), 
    text: newTask.value, 
    done: false
  })
  newTask.value = ''
}

const deleteTask = (id) => {
  tasks.value = tasks.value.filter(t => t.id !== id)
}

const showOnlyPending = ref(false)
const filteredTask = computed(() => showOnlyPending.value ? tasks.value.filter(t => !t.done) : tasks.value)

</script>

<template>
  <header class="app-header">
    <h1 class="header">WeToDoList.com</h1>
  </header>

<div class="app">
<h1>What To Do List : </h1>

  <form @submit.prevent="addTask" class="form">
    <input v-model="newTask" placeholder="Tambah kegiatan baru"/>
    <button type="submit">Add</button>
  </form>

  <label class="filter">
    <input type="checkbox" v-model="showOnlyPending" />Tampilkan hanya yang belum selesai
  </label>

  <ul class="task-list">
    <li v-for="task in filteredTask" :key="task.id" class="task">
      <input type="checkbox" v-model="task.done" />
      <span :class="{done: task.done}">{{ task.text }}</span>
      <button @click="deleteTask(task.id)">cancel/delete</button>
    </li>
  </ul>
</div>

  <footer>
    <p>Widuri-233510403</p>
    <p>Pemrograman Berbasis Komponen</p>
  </footer>
</template>

<style scoped>
.task span.done {
  text-decoration: line-through;
  color: palevioletred;
}
</style>