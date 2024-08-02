<template>
    <div class="dropdown" ref="dropdown">
      <button class="dropdown-toggle" @click="toggleMenu">{{ title }}</button>
      <div class="dropdown-menu" v-if="isOpen">
        <a class="dropdown-item" v-for="item in items" :key="item" @click="selectItem(item)">
          {{ item }}
        </a>
      </div>
    </div>
  </template>
  
  <script setup>
    import { ref, onMounted, onUnmounted, nextTick } from 'vue';

    const props = defineProps({
    title: {
        type: String,
        default: 'Menu'
    },
    items: {
        type: Array,
        default: () => []
    }
    });

    const emit = defineEmits(['itemSelected']);
    const isOpen = ref(false);
    const dropdown = ref(null);

    const toggleMenu = () => {
  isOpen.value = !isOpen.value;
};

const selectItem = (item) => {
  isOpen.value = false;
  emit('itemSelected', item);
};

const handleClickOutside = (event) => {
  if (dropdown.value && !dropdown.value.contains(event.target)) {
    isOpen.value = false;
  }
};

onMounted(() => {
  nextTick(() => {
    document.addEventListener('click', handleClickOutside);
  });
});

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside);
});
</script>
  
  <style scoped>
  .dropdown {
    position: relative;
    display: inline-block;
  }
  
  .dropdown-toggle {
    background-color: #ffffff;
    color: rgb(0, 0, 0);
    padding: 10px;
    border: none;
    cursor: pointer;
  }
  
  .dropdown-menu {
    display: block;
    position: absolute;
    background-color: white;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    z-index: 1;
    min-width: 160px;
  }
  
  .dropdown-item {
    padding: 12px 16px;
    display: block;
    color: black;
    text-decoration: none;
    cursor: pointer;
  }
  
  .dropdown-item:hover {
    background-color: #f1f1f1;
  }
  </style>
  