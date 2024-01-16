<script setup>
  import Books from './components/Books.vue';
  import BookProgress from './components/BookProgress.vue';
  import AddBook from './components/AddBook.vue';

  import { ref, reactive } from 'vue';

const books = reactive([
    {
      id: 1,
      title: "Dom Quixote",
      cover:
        "https://m.media-amazon.com/images/I/71LzWaIbBoL._SY425_.jpg",
      isRead: false,
      isbn: "8595200858",
      author: "Miguel De Cervantes",
    },
    {
      id: 2,
      title: "O Senhor dos Anéis: A Sociedade do Anel",
      cover:
        "https://m.media-amazon.com/images/I/81hCVEC0ExL._SY425_.jpg",
      isRead: true,
      isbn: "8595084750",
      author: "J.R.R. Tolkien",
    },
    {
      id: 3,
      title: "O Pequeno Príncipe",
      cover: "https://m.media-amazon.com/images/I/81MscdgdwLL._SY425_.jpg",
      isRead: true,
      isbn: "8595081514",
      author: "Antoine de Saint-Exupéry",
    },
    {
      id: 4,
      title: "Harry Potter e a Pedra Filosofal",
      cover: "https://m.media-amazon.com/images/I/41897yAI4LL._SY445_SX342_.jpg",
      isRead: false,
      isbn: "8532530788",
      author: "J.K. Rowling",
    },
  ])

  let showAddBook = ref(false);

  function toggleBookReadStatus(id){
    books.forEach((book) => {
      if(book.id == id){
        book.isRead = !book.isRead;
      }
    })
  }
  
  function saveBook(newBook){

    if (!newBook.title.trim()) {
        alert("O título é obrigatório.");
        return false;
    }

    if (!newBook.cover.trim()) {
        alert("A URL da capa é obrigatória.");
        return false;
    }

    if (!newBook.author.trim()) {
        alert("O autor é obrigatório.");
        return false;
    }

    if (!/^\d+$/.test(newBook.isbn)) {
        alert("O ISBN deve conter apenas números.");
        return false;
    }
  

    newBook.id = Math.max(...books.map((el) => el.id)) + 1;
    books.push(newBook);
    showAddBook.value = false;
  }

  function removeBook(idBookToRemove){
    const indexToRemove = books.findIndex((book) => book.id === idBookToRemove);

    if (indexToRemove !== -1) {
      books.splice(indexToRemove, 1);
    }
  }

</script>

<template>
  <div class="container" v-if="!showAddBook">
    <h1>📚 Meus Livros</h1>
    <div class="header-btns">
      <button @click="showAddBook = true"
        class="btn"
        
      >
        Adicionar Livro +
      </button>
    </div>
 
    <div class="books-container">
      <Books @removeBook="removeBook" @toggleBookReadStatus="toggleBookReadStatus" :books="books" />

      <BookProgress :books="books"></BookProgress>
    </div>
    
  </div>
  <div v-else class="container">
      <AddBook @saveBook="saveBook" @closeAddBook="showAddBook = false"/>
    </div>
  
</template>

<style scoped>
  
  .container .books-container {
    margin-top: 50px;
  }
</style>