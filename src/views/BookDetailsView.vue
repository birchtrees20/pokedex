<script setup>
import { ref, onMounted } from 'vue'
import BookService from '@/services/BookService.js'

const theBook = ref(null)
// const id = ref(100001)

const props = defineProps({
    id: { required: true }
})

onMounted(() => {
    //BookService.getBook(id.value)
    BookService.getBook(props.id)
    .then((response)=>{
        theBook.value = response.data
    })
    .catch((error)=>{
        console.log(error)
    })
})
</script>

<template>
    <div class="detail" v-if="theBook">
        <h1>{{  theBook.name }} ({{  theBook.id }})</h1>
        <img v-if="book" :src="book.image" alt="">
        <h2>Type</h2>
        <p>{{  theBook.type1 }},  {{  theBook.type2 }}</p>
        <h2>Japanese Name</h2>
        <p>{{  theBook.japname }}</p>
        <h2>Evolution</h2>
        <p>{{  theBook.evolution }}</p>
    </div>
</template>

<style>
.detail h1 {
    text-align: center;
}
</style>

