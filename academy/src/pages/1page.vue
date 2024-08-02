<template>
    <div class="form-container">
      <h2>Форма</h2>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="date">Дата:</label>
          <input type="date" v-model="form.date" id="date" required />
        </div>
        <div class="form-group">
          <label for="text">Текст:</label>
          <textarea v-model="form.text" id="text" required></textarea>
        </div>
        <div class="form-group">
          <label for="select">Выбор:</label>
          <select v-model="form.select" id="select" required>
            <option value="" disabled>Выберите один</option>
            <option value="option1">Опция 1</option>
            <option value="option2">Опция 2</option>
            <option value="option3">Опция 3</option>
          </select>
        </div>
        <button type="submit">Сохранить</button>
      </form>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import axios from 'axios';
  
  const form = ref({
    date: '',
    text: '',
    select: ''
  });
  
  const submitForm = async () => {
    try {
      await axios.post('http://localhost:3000/submit', form.value);
      alert('Форма успешно отправлена!');
      form.value = { date: '', text: '', select: '' };
    } catch (error) {
      console.error('Ошибка при отправке формы:', error);
      alert('Произошла ошибка при отправке формы.');
    }
  };
  </script>
  
  <style scoped>
  .form-container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: #f9f9f9;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input, textarea, select {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  button {
    background-color: #3498db;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #2980b9;
  }
  </style>
  
  