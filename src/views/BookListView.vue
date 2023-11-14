<script setup>
import { ref, onMounted } from 'vue'
import ProductCard from '@/components/ProductCard.vue'
// import axios from 'axios'  // Don't need this anymore, will use via the service
import BookService from '@/services/BookService.js'

const books = ref(null)

onMounted(() => {
  BookService.getBooks()
  .then((response)=> {
    books.value = response.data
  })
  .catch((error) => {
    console.log(error)
  })
})
</script>

<template>
  <div class="products">
    <ProductCard v-for="book in books" :key="book.id" :book="book" />
  </div>
</template>

<style>
.products {
  justify-content: center;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  place-items: center;
}

body {
  display: flex;
  justify-content: center;
  font-family: Arial, Helvetica, sans-serif;
}
</style>

