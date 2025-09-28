<script setup>
import { ref } from 'vue';
import Form from './Form.vue';
import HelloWorld from './HelloWorld.vue';

const showForm = ref(true);
const showHelloWorld = ref(false);
const showFavorites = ref(false);

const openForm = () => {
  showForm.value = true;
  showHelloWorld.value = false;
  showFavorites.value = false;

  document.getElementsByClassName('form').item(0).classList.add('active');
  document.getElementsByClassName('xDDD').item(0).classList.remove('active');
  document.getElementsByClassName('Hello').item(0).classList.remove('active');
};

const openLink1 = () => {
  showForm.value = false;
  showHelloWorld.value = true;
  showFavorites.value = false;
  
    document.getElementsByClassName('form').item(0).classList.remove('active');
  document.getElementsByClassName('xDDD').item(0).classList.add('active');
  document.getElementsByClassName('Hello').item(0).classList.remove('active');
};

const openLink2 = () => {
  showForm.value = false;
  showHelloWorld.value = false;
  showFavorites.value = true;

    document.getElementsByClassName('form').item(0).classList.remove('active');
  document.getElementsByClassName('xDDD').item(0).classList.remove('active');
  document.getElementsByClassName('Hello').item(0).classList.add('active');
};
</script>

<template>
  <div class="nav">
    <nav>
      <button type="submit" @click="openForm" class="form">All Meetups</button>
      <button type="submit" @click="openLink1" class="xDDD">Add New Meetup</button>
      <button type="submit" @click="openLink2" class="Hello">My Favorites</button>
    </nav>
  </div>

  <Form v-if="showForm" />
  <HelloWorld v-if="showHelloWorld" />
  <p v-if="showFavorites">Favorites Content Here</p>
</template>
<style scoped>
div.nav {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 5em;
  margin-bottom: 3em;
  overflow: hidden;
  padding: 0;
  background-color: #212121; /* Primary dark gray */
}

nav {
  padding: 1rem;
}

nav {
  display: flex;
  gap: 1rem;
  margin: 0;
  padding: 0;
}

button {
  margin: 0;
  height: 5em;
  width: 10em;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #212121; /* Primary dark gray */
  color: #FFFFFF; /* White */
  border: none;
  border-radius: 5px;
  transition: all 0.3s ease;
}

a {
  color: #FFFFFF; /* White */
  text-decoration: none;
  font-weight: bold;
}

button:hover {
  cursor: pointer;
  background-color: #333333;
}

button.active {
  border: 1px solid #64FFDA; /* Teal */
}

/* button:active {
  background-color: #2e5276b7;
  transform: scaleX(0.85) scaleY(0.78);
  box-shadow: 2px 5px 32px rgb(16, 107, 205);
  border-radius: 20px;
  transition: all 0.27s ease-in-out;
  filter: drop-shadow(0 0 2em #42b883aa);
} */

</style>