<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

const tasks = ref([]);
const title = ref('');
const todo = ref('');
const date = ref('');
const formattedDate = ref('');
const hasLoaded = ref(false);
const router = useRouter();
const taskToRemove = ref(null);
const taskToChange = ref(null);

onMounted(() => {
  hasLoaded.value = true;
});

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
    formattedDate.value = '';
  }
};

const updateFormattedDate = () => {
  formattedDate.value = date.value;
};

const showmore = (index) => {
  router.push({ path: `/task/${index}` });
};

const removeTask = (index) => {
  taskToRemove.value = index;
  setTimeout(() => {
    tasks.value.splice(index, 1);
    taskToRemove.value = null;
  }, 300); 
};

const changeTask = (index) => {
  const task = tasks.value[index];
  title.value = task.title;
  todo.value = task.todo;
  date.value = task.date;
  taskToChange.value = index;
  setTimeout(() => {
    tasks.value.splice(index, 1);
    taskToChange.value = null;
  }, 300);
};
</script>

<template>
  <div class="app" :class="{ 'fade-in': hasLoaded }">
    <form @submit.prevent="handleSubmit" class="form">
      <div class="input-container">
        <input type="text" v-model="title" id="title" required />
        <label for="title">Task name</label>
      </div>

      <div class="input-container">
        <input type="text" v-model="todo" id="todo" required />
        <label for="todo">Task</label>
      </div>
      <div class="input-container">
        <input type="text" id="date" v-model="date" @change="updateFormattedDate" required />
        <label for="date">When</label>
      </div>
      <p>Selected Date: {{ formattedDate }}</p>
      <button type="submit">Add Task</button>
    </form>
  </div>
  <div class="component" v-if="tasks.length > 0">
    <div
      class="task"
      v-for="(task, index) in tasks"
      :key="index"
      :class="{ 'fade-out': taskToRemove === index || taskToChange === index }"
    >
      <strong>Title: {{ task.title }}</strong>
      <strong>Task: {{ task.todo }}</strong>
      <strong>Date: ({{ task.date }})</strong>
      <button type="button" class="changebut" @click="changeTask(index)">=</button>
      <button type="button" class="button_X" @click="removeTask(index)">x</button>
      <button @click="() => showmore(index)" class="button">Show me more</button>
    </div>
  </div>
  <p v-else id="keyframesTry" :class="{ 'typing-animation': hasLoaded }">No tasks yet</p>
</template>

<style scoped>
.button_X {
  display: flex;
  justify-content: right;
  height: 1.5em;
  width: 1.5em;
  background-color: #ff4d4d;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  align-items: center;
  font-weight: bold;
  color: whitesmoke;
  font-size: 1em;
  padding-right: 7px;
  margin: 0;
  text-align: center;
  position: absolute;
  top: 0.5em;
  right: 0.5em;
  transition: all 0.3s ease;
}
.changebut {
  display: flex;
  justify-content: right;
  height: 1.5em;
  width: 1.5em;
  background-color: #9eac09;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  align-items: center;
  font-weight: bold;
  color: whitesmoke;
  font-size: 1em;
  padding-right: 7px;
  margin-right: 30px;
  text-align: center;
  position: absolute;
  top: 0.5em;
  right: 0.5em;
  transition: all 0.3s ease;
}
.button_X:hover {
  background-color: #ff3328;
  filter: drop-shadow(0 0 1em #ff3328aa);
  transform: scale(1.1);
}
.fade-in {
  animation: fadeIn 0.5s ease-in-out forwards;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes fadeBlock {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }

  to {
    opacity: 1;
    transform: translateY(0) ;
  }
  
}

p#keyframesTry {
  font-size: 1.5em;
  color: white;
  width: fit-content;
  margin: auto;
  white-space: nowrap;
  overflow: hidden;
  border-right: 3px solid;
  width: 12ch;
}

.typing-animation {
  animation: typing 2s steps(20) 1 forwards alternate;
}

@keyframes typing {
  from {
    width: 0ch;
  }

  to {
    width: 12ch;
  }
}

.input-container {
  position: relative;
  margin-bottom: 15px;
}

label {
  position: absolute;
  top: 0;
  left: 10px;
  color: white;
  pointer-events: none;
  transition: all 0.5s ease;
}

input {
  padding: 8px;
  font-size: 14px;
  background-color: #2f2c2c;
  color: white;
  border: none;
  border-bottom: 2px solid #666;
  width: 100%;
  box-sizing: border-box;
  transform: all 0.4s ease;
}

input:focus {
  outline: none;
  border-bottom: 2px solid rgb(8, 88, 158);
  filter: drop-shadow(0 0 1em #427bb8aa);
  transition: filter 0.3s ease;
}

input:focus+label,
input:valid+label {
  transform: translateY(-20px);
  font-size: 0.8em;
  color: aliceblue;
}

.component {
  margin: auto;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  font-family: sans-serif;
  font-size: 0.9em;
  color: white;
  padding: 10px;
  border-radius: 10px;
  width: 90vw;
  height: auto;
  gap: 22px;
  flex-wrap: wrap;
  background-color: #212121; /* Primary dark gray */
}

.task {
  margin: 5px 0;
  padding: 10px;
  border-radius: 5px;
  width: 15vw;
  text-align: left;
  justify-content: right;
  align-items: right;
  box-shadow: 0 0px 4px rgba(54, 51, 88, 0.602);
  padding: 20px;
  display: flex;
  align-items: right;
  flex-direction: column;
  gap: 15px;
  text-wrap: wrap;
  overflow: hidden;
  transition: all 0.48s ease-in-out, z-index 0s 0.5s;
  z-index: 1;
  animation: fadeBlock 0.7s ease-in-out forwards;
  position: relative;
  opacity: 0.8;
  background-color: #333333;
  color: #FFFFFF;
}

.app {
  max-width: 400px;
  margin: 20px auto;
  font-family: sans-serif;
  color: #FFFFFF;
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
.fade-out {
  animation: fadeOut 0.5s ease-out forwards;
}

@keyframes fadeOut {
  from {
    opacity: 0.8;
    transform: translateY(0);
  }
  to {
    opacity: 0;
    transform: translateY(-20px);
  }
}
</style>