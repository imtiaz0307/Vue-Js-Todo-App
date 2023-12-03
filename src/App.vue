<script setup>
import Navbar from './components/navbar.vue';
import Todos from './components/todos.vue';
import { ref } from "vue"

const darkMode = ref(true)

const toggleDarkMode = () => darkMode.value = !darkMode.value

</script>

<template>
  <main :class="{ main: true, light_theme: !darkMode, dark_theme: darkMode }">
    <Navbar :toggleTheme="toggleDarkMode" :isDark="darkMode" />
    <Todos />
  </main>
</template>

<style>
.main {
  min-height: 100vh;
  transition: 250ms;
  background-color: var(--color-bg);
  padding-bottom: 2.5rem;
  margin-bottom: 0;
  overflow: hidden;
}

.light_theme {
  --color-bg: #fff;
  --color-modal-overlay: #ffffff2e;
  --color-primary: #5926f0;
  --color-secondary: #a9a9a9;
  --color-text: #111;
  --box-shadow-color: #e9e9e9;
}

.dark_theme {
  --color-bg: #0c0324;
  --color-modal-overlay: #110d1d2e;
  --color-primary: #5926f0;
  --color-secondary: #a9a9a9;
  --color-text: #fff;
  --box-shadow-color: #474747;
}
</style>