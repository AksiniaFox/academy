<script setup>
import Menu from './components/menu/menu.vue';
</script>

<template>
  <div id="app">
    <Menu />
    <router-view />
  </div>
</template>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

