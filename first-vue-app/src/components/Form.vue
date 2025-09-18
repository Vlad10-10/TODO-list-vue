<script setup>
import { ref } from 'vue';

const tasks = ref([]);

const title = ref('');
const todo = ref('');
const date = ref('');

function showmore() {
  const main = document.querySelector('.task');
  main.classList.toggle('active');

}

const handleSubmit = () => {
  if (title.value === '' || todo.value === '' || date.value === '') {
    alert('Please fill in all fields');
  } else {
    tasks.value.push({
      title: title.value,
      todo: todo.value,
      date: date.value,
    });

    console.log('Task added:', title.value, todo.value, date.value);

    title.value = '';
    todo.value = '';
    date.value = '';
  }
};

openForm = () => {
  return `<div class="component" v-if="tasks.length > 0">
    <div class="task" v-for="(task, index) in tasks" :key="index">
      <strong>Title: {{ task.title }}</strong>
      <strong>Task: {{ task.todo }}</strong>
      <strong>Date: ({{ task.date }})</strong>
      <button @click="showmore" class="button">Show me more</button>
    </div>
  </div>
  <p v-else>No tasks yet</p>
  <div class="app">
    <form @submit.prevent="handleSubmit" class="form">
      <div class="input-container">
        <input type="text" v-model="title" id="title" required />
        <label for="title">Title</label>
      </div>

      <div class="input-container">
        <input type="text" v-model="todo" id="todo" required />
        <label for="todo">Todo</label>
      </div>
      <input type="date" v-model="date" />
      <button type="submit">Add Task</button>
    </form>
  </div>;`
}
</script>
<template>
  <div class="component" v-if="tasks.length > 0">
    <div class="task" v-for="(task, index) in tasks" :key="index">
      <strong>Title: {{ task.title }}</strong>
      <strong>Task: {{ task.todo }}</strong>
      <strong>Date: ({{ task.date }})</strong>
      <button @click="showmore" class="button">Show me more</button>
    </div>
  </div>
  <p v-else>No tasks yet</p>
  <div class="app">
    <form @submit.prevent="handleSubmit" class="form">
      <div class="input-container">
        <input type="text" v-model="title" id="title" required />
        <label for="title">Title</label>
      </div>

      <div class="input-container">
        <input type="text" v-model="todo" id="todo" required />
        <label for="todo">Todo</label>
      </div>
      <input type="date" v-model="date" />
      <button type="submit">Add Task</button>
    </form>
  </div>
</template>

<style scoped>
.input-container {
  position: relative;
  margin-bottom: 15px; /* Add some spacing between input groups */
}

label {
  position: absolute;
  top: 0;
  left: 10px;
  color: white;
  pointer-events: none;
  transition: all 0.3s ease;
}

input {
  padding: 8px;
  font-size: 14px;
  background-color: #2f2c2c;
  color: white; /* Add text color */
  border: none;
  border-bottom: 2px solid #666; /* Add a subtle bottom border */
  width: 100%; /* Make the input take the full width */
  box-sizing: border-box; /* Include padding and border in the element's total width and height */
  transform: all 0.4s ease;

}

input:focus {
  outline: none; /* Remove the default focus outline */
  border-bottom: 2px solid rgb(8, 88, 158); /* Highlight the bottom border on focus */
  filter:drop-shadow(0 0 1em #427bb8aa);
  transition: filter 0.3s ease;
}

input:focus + label,
input:valid + label {
  transform: translateY(-20px);
  font-size: 0.8em;
  color: aliceblue;
}

.component {
  margin: auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: left;
  font-family: sans-serif;
  font-size: 0.9em;
  color: white;
  padding: 10px;
  border-radius: 10px;
  width: 95vw;
  height: auto;
  gap: 15px;
}

.task {
  margin: 5px 0;
  padding: 10px;
  border-radius: 5px;
  width: 15vw;
  text-align: left;
  justify-content: right;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
  padding: 20px;
  display: flex;
  align-items: right;
  flex-direction: column;
  gap: 15px;
  text-wrap: wrap;
  overflow: hidden;
  transition: all 0.48s ease-in-out;
}

.app {
  max-width: 400px;
  margin: 20px auto;
  font-family: sans-serif;
}

form {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 16px;
}

button {
  padding: 8px;
  font-size: 14px;
  background-color: #2f2c2c;
}

.task.active {
  z-index: 1;
  height: 80vh;
  width: 95vw;
  transition: all 0.48s ease-in-out;
  margin-top: 10em;
  position: absolute;
  background-color: #242424;
  padding: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.85);
  font-size: 3em;
}

.button {
  background-color: #1a1a4b;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  border: 1px solid white;
  transition: all 0.48s ease-in-out;
  width: 10vw;
  display: flex;
  align-items: center;
  justify-content: center;
}

.button:hover {
  background-color: #333366;
  filter: drop-shadow(0 0 1em #427bb8aa);
}

.button:active {
  animation: ButtonAnim 0.7s ease-in-out infinite;
}

@keyframes ButtonAnim {
  0% {
    transform: rotate(0deg) scale(1);
  }

  33% {
    transform: rotate(-2deg) scale(1.02);
  }

  66% {
    transform: rotate(2deg) scale(1.02);
  }

  100% {
    transform: rotate(0deg) scale(1);
  }
}
</style>