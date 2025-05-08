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
/*Header*/ 
.app-header {
  position: fixed;
  top: 0;
  left: 0;
  padding: 0.2rem 1rem;
  background-color: palevioletred;
  border-bottom-right-radius: 6px;
  width: 100%;
  font-family: 'Playfair Display';
  font-size: 1.25rem;
  font-weight: 600;
  letter-spacing: 1px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

.header{
  color: white;
}

/*Body*/
.app {
  max-width: 500px;
  margin: 100px auto 100px;
  padding: 2rem;
  background-color: #fff8f4;
  border-radius: 16px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
  font-family: 'Inter', sans-serif;
  color: #333;
}

h1 {
  font-size: 2rem;
  font-weight: 600;
  text-align: center;
  margin-bottom: 1.5rem;
  color: palevioletred;
}

/*Form Input*/
.form {
  display: flex;
  gap: 1rem; 
  margin-bottom: 1rem;
  position: sticky;
  top: 0;
  background-color: #fff8f4;
  z-index: 1;
  padding: 1rem;
  justify-content: center; 
}

input[type="text"] {
  flex: 1; 
  padding: 0.75rem 1rem; 
  border: 2px solid #f2c6c2;
  border-radius: 8px;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.2s;
}

input[type="text"]:focus {
  border-color: #b53f70;
}

button[type="submit"] {
  background-color: palevioletred;
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
  transition: background-color 0.2s;
}


button[type="submit"]:hover {
  background-color: rgb(177, 81, 113);
}

/*Filter Checkbox*/
.filter {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.95rem;
  margin-bottom: 1rem;
  color: palevioletred;
}

/*Task List*/
.task-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #fff;
  padding: 0.75rem 1rem;
  border: 1px solid #ffe1de;
  border-radius: 8px;
  margin-bottom: 0.5rem;
  transition: background-color 0.2s;
}

.task:hover {
  background-color: #fff2f0;
}

.task input[type="checkbox"] {
  margin-right: 0.75rem;
  transform: scale(1.2);
}

.task span {
  flex: 1;
  font-size: 1rem;
}

.task span.done {
  text-decoration: line-through;
  color: palevioletred;
}

.task button {
  background: transparent;
  border: none;
  color: palevioletred;
  font-weight: bold;
  cursor: pointer;
  font-size: 0.9rem;
  transition: color 0.2s;
}

.task button:hover {
  color: rgb(177, 81, 113);
}

/*Footer*/
footer {
  background-color: palevioletred;
  color: white;
  width: 100%;
  font-family: 'Playfair Display', serif;
  position: fixed;
  bottom: 0;
  left: 0;
  text-align: center;
  padding: 10px;
}

footer p {
  margin: 0;
}
</style>