<template>
  <div class="container mt-5">
    <h1 class="text-center mb-4">Моя коллекция событий</h1>
    
    <!-- Форма добавления карточки -->
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <form @submit.prevent="addBook" class="input-group mb-4">
          <input 
            v-model="newBookTitle" 
            type="text" 
            class="form-control" 
            placeholder="Название события"
            required
          >
          <input 
            v-model="newBookDescription" 
            type="text" 
            class="form-control" 
            placeholder="Описание"
          >
          <input 
            v-model="newBookImage" 
            type="text" 
            class="form-control" 
            placeholder="Ссылка на изображение"
          >
          <button class="btn btn-primary" type="submit">Добавить</button>
        </form>
      </div>
    </div>

    <!-- Кнопка сортировки -->
    <div class="row mb-3">
      <div class="col-md-6 offset-md-3 text-center">
        <button class="btn btn-secondary" @click="sortBooks">Сортировать по названию</button>
      </div>
    </div>

    <!-- Список карточек -->
    <div class="row">
      <div v-for="book in books" :key="book.id" class="col-md-4 mb-3">
        <div class="card h-100">
          <img :src="book.image" class="card-img-top" alt="Событие" />
          <div class="card-body">
            <h5 class="card-title">{{ book.title }}</h5>
            <p class="card-text">{{ book.description }}</p>
            <button @click="removeBook(book.id)" class="btn btn-sm btn-danger">Удалить</button>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'

const books = ref([])
const newBookTitle = ref('')
const newBookDescription = ref('')
const newBookImage = ref('')

const addBook = () => {
  books.value.push({
    id: Date.now(),
    title: newBookTitle.value,
    description: newBookDescription.value,
    image: newBookImage.value || 'https://via.placeholder.com/150'
  })
  newBookTitle.value = ''
  newBookDescription.value = ''
  newBookImage.value = ''
}

const removeBook = (id) => {
  books.value = books.value.filter(book => book.id !== id)
}

// Сортировка по названию
const sortBooks = () => {
  books.value.sort((a, b) => a.title.localeCompare(b.title))
}
</script>