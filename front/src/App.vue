<template>
  <section>
    <card v-for="book of books" 
    :key="book.id" 
    :book="book" 
    @delete-book="deleteBook"></card>
  </section>
</template>

<script>
import http from './http-common'
export default {
  data() {
    return {
      books: []
    }
  },
  methods: {
    getBook() {
      http.get('/books').then( (response) => {
        this.books = response.data;
      });
    },
    deleteBook(bookId) {
      http.delete('/books/' + bookId).then( () => {
        this.books = this.books.filter( (book) => book.id !== bookId)
      })
    }
  },
  mounted() {
    this.getBook();
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
