<script setup>
import HelloWorld from './components/HelloWorld.vue'
import MainNav from './components/MainNaigation.vue'
import FormMain from './components/Form.vue'
</script>

<template>
  <MainNav />
  
</template>

<style scoped>
body {
  background-color: #121212; /* Dark gray */
  color: #FFFFFF; /* White */
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #64FFDA); /* Teal */
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #64FFDA); /* Teal */
}
</style>
