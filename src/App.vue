<script setup>
// Vue 3 <script setup> format
import { ref } from 'vue'

// Reactive state for new todo input
const newTodo = ref('')

// Reactive list of todos
const todos = ref([])

// Method to add a new todo
const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: Date.now(), // unique ID based on timestamp
      text: newTodo.value.trim(),
      completed: false
    })
    newTodo.value = '' // clear input after adding
  }
}

// Method to delete a todo by its ID
const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}
</script>

<template>
  <header>
    <h1>Welcome to our ToDo web app</h1>
  </header>

     <div class="app">
    <h1>Things to finish TODAY</h1>

    <!-- Input for adding a new todo -->
    <div class="input-container">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        placeholder="Add a new todo..."
        class="todo-input"
      />
    </div>

    <!-- Message shown if there are no todos -->
    <div v-if="todos.length === 0" class="empty">
      No todos yet. Add one above.
    </div>

    <!-- Render each todo item -->
    <div
      v-for="todo in todos"
      :key="todo.id"
      class="todo-item"
    >
      <input
        type="checkbox"
        v-model="todo.completed"
        class="todo-checkbox"
      />
      <span :class="{ completed: todo.completed }" class="todo-text">
        {{ todo.text }}
      </span>
      <button @click="deleteTodo(todo.id)" class="delete-btn">
        ×
      </button>
    </div>
  </div>
  
</template>

<style scoped>
/* Global layout reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #fafafa;
  color: #333;
  line-height: 1.6;
}

.app {
  max-width: 500px;
  margin: 60px auto;
  padding: 0 20px;
}

h1 {
  text-align: center;
  font-weight: 300;
  font-size: 2rem;
  margin-bottom: 40px;
  color: #666;
}

.input-container {
  margin-bottom: 30px;
}

.todo-input {
  width: 100%;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
  background: white;
}

.todo-input:focus {
  outline: none;
  border-color: #333;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 15px 0;
  border-bottom: 1px solid #eee;
}

.todo-item:last-child {
  border-bottom: none;
}

.todo-checkbox {
  margin-right: 15px;
  width: 18px;
  height: 18px;
  cursor: pointer;
}

.todo-text {
  flex: 1;
  font-size: 16px;
  transition: all 0.3s ease;
}

.todo-text.completed {
  text-decoration: line-through;
  color: #999;
}

.delete-btn {
  background: none;
  border: none;
  color: #ccc;
  cursor: pointer;
  font-size: 18px;
  padding: 5px;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.todo-item:hover .delete-btn {
  opacity: 1;
}

.delete-btn:hover {
  color: #ff4444;
}

.empty {
  text-align: center;
  color: #999;
  font-style: italic;
  margin-top: 40px;
}
</style>
