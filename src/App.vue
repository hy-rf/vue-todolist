<script setup>
import { ref } from "vue";

const text = ref("");
const todos = ref([]);
function addTodo() {
  todos.value.push({
    isCompleted: false,
    text: text.value,
  });
  text.value = "";
}
function deleteTodo(index) {
  todos.value.splice(index, 1);
}
</script>

<template>
  <div class="app-container">
    <header class="header">
      <h1>Todo List</h1>
    </header>
    <div class="input-container">
      <input v-model="text" type="text" placeholder="Add a new task..." />
      <button @click="addTodo">Add</button>
    </div>
    <div class="todos">
      <div v-for="(item, index) in todos" :key="index" class="todo-item">
        <input
          type="checkbox"
          :checked="item.isCompleted"
          v-model="item.isCompleted"
        />
        <p :class="{ completed: item.isCompleted }">{{ item.text }}</p>
        <button @click="deleteTodo(index)">Delete</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.header {
  text-align: center;
  margin-bottom: 20px;
}

.input-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

button {
  padding: 10px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.todos {
  margin-top: 20px;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

.todo-item p {
  margin: 0;
}

.completed {
  text-decoration: line-through;
  color: #aaa;
}
</style>
