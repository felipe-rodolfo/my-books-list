<script setup>

const props = defineProps(['books']);

</script>

<template>
    <div class="books-list">
        <div class="book" v-for="book in books" :key="book.isbn">
            <button @click="$emit('removeBook', book.id)" class="removeBook"><i class="fa-solid fa-xmark"></i></button>
            <div class="readIt" v-if="book.isRead">
                <i class="fa-solid fa-eye"></i>
            </div>
            <div class="book-cover">
                <img :src="book.cover" />
    
                <button @click="$emit('toggleBookReadStatus', book.id)" :class="{isRead : book.isRead}">
                    <i class="fa-solid fa-eye"></i>
                    <span>{{ book.isRead ? 'Já li' : 'Ainda não li'}}</span
                >
            </button>
          </div>
          <div class="book-details">
            <p class="book-author">{{book.author}}</p>
            <h3 class="book-title">{{book.title}}</h3>
            <p><i class="fa-solid fa-hashtag icon"></i> {{book.isbn}}</p>
          </div>
        </div>
    </div>
</template>

<style scoped>
.book {
  height: 100%;
  display: flex;
  flex-direction: column;
  text-align: center;
  position: relative;
}
 
.book .book-cover {
  position: relative;
}
.book .book-cover img {
  width: 100%;
  min-height: 413px;
  height: 100%;
  object-fit: cover;
  box-shadow: 0px 4px 11px 0px rgb(0 0 0 / 14%);
}
 
.book .book-cover:hover button {
  visibility: visible;
  opacity: 1;
}
 
.book .book-cover button {
  visibility: hidden;
  display: block;
  position: absolute;
  transition: opacity 0.4s ease-in-out, visibility 0.4s ease-in-out;
  transform: none;
  width: 100%;
  left: 0;
  bottom: 0;
  text-align: center;
  opacity: 0;
  border: none;
  background-color: rgb(232, 93, 65);
  color: white;
  height: 51px;
  cursor: pointer;
}
 
.book .book-cover button.isRead {
  background-color: #1cab47;
}
 
.book .book-cover button span {
  font-weight: 500;
  font-size: 18px;
  margin-left: 10px;
}
 
.book .book-title {
  font-size: 21px;
  line-height: 27px;
  margin-bottom: 10px;
}
 
.book .book-author {
  font-size: 19px;
  line-height: 26px;
  margin-bottom: 10px;
}
 
.book .book-details {
  padding: 10px 20px;
  display: flex;
  flex-direction: column;
  width: 100%;
}
 
.book .readIt {
  padding: 10px 20px;
  position: absolute;
  left: auto;
  right: 5px;
  bottom: auto;
  top: 5px;
  z-index: 10;
  border-radius: 25px;
  overflow: hidden;
  background-color: #1cab47;
  color: white;
}

.book .removeBook {
  padding: 10px 20px;
  position: absolute;
  left: 5px;
  bottom: auto;
  top: 5px;
  z-index: 10;
  border-radius: 25px;
  border: none;
  background-color: #c0392b;
  color: white;
  cursor: pointer;
  transition: all ease 0.3s;
}

.book .removeBook:hover {
  transform: scale(1.1);
}
 
.books-list {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr;
  gap: 20px;
}
 

@media (max-width: 768px) {
  .books-list {
    grid-template-columns: 1fr 1fr;
  }
}
 
@media (max-width: 576px) {
  .books-list {
    grid-template-columns: 1fr;
  }
}
</style>