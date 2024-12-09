<script setup>
import { ref } from "vue";

const newTask = ref(""); 
const tasks = ref([]); 


function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value, completed: false });
    newTask.value = "";
  }
}


function toggleTask(index) {
  tasks.value[index].completed = !tasks.value[index].completed;
}


function removeTask(index) {
  tasks.value.splice(index, 1);
}
</script>

<template>
  <div id="app" class="container mt-5">
    <h1 class="text-center mb-4">Мой список задач</h1>
    
    
    <div class="card mb-4">
      <div class="card-body d-flex">
        <input
          class="form-control me-2"
          type="text"
          v-model="newTask"
          @keyup.enter="addTask"
          placeholder="Добавьте новую задачу"
        />
        <button class="btn btn-success" @click="addTask">Добавить</button>
      </div>
    </div>

    
    <ul class="list-group">
      <li
        v-for="(task, index) in tasks"
        :key="index"
        class="list-group-item d-flex justify-content-between align-items-center"
      >
        <span
          :class="{ 'text-decoration-line-through text-muted': task.completed }"
          @click="toggleTask(index)"
          style="cursor: pointer;"
        >
          {{ task.text }}
        </span>
        <button class="btn btn-danger btn-sm" @click="removeTask(index)">Удалить</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.completed {
  cursor: pointer;
}

.text-decoration-line-through {
  text-decoration: line-through;
}
</style>