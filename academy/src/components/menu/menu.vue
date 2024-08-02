<template>
    <header class="header">
      <DropdownMenu class = "menu" title="Меню" :items="menuItems" @itemSelected="handleSelection" />
      <div  class="logo"><h1>Техническая академия</h1></div>
    </header>
  </template>
  
  <script>
  import DropdownMenu from './dropdown.vue';
  import { useRouter } from 'vue-router';
  
  export default {
    name: 'Header',
    components: {
      DropdownMenu
    },
    setup() {
      const router = useRouter();
      const menuItems = ['Главная', 'Форма', 'Задание'];

      const handleSelection = (item) => {
        console.log('Selected item:', item);
        if (item === 'Главная') {
          router.push('/');
        } else if (item === 'Форма') {
          router.push('/page1');
        } else if (item === 'Задание') {
          router.push('/page2');
        }
      };

      return {
        menuItems,
        handleSelection
      };
  }
};
  </script>
  
  <style scoped>
  .header {
    display: flex;
    align-items: center;
    padding: 10px 20px;
    background-color: #2c3e50;
    color: white;
  }
  
  .logo {
    margin: 0;
    font-size: 1.1em;
    margin-left: auto;
    margin-right: auto;

  }

  .menu {
    display: flex;
    justify-content: flex-start;
  }
  </style>
  