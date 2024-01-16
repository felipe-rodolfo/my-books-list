<script setup>
    import { ref } from 'vue';

    let newBook = ref({
        title: "",
        cover: "",
        isRead: false,
        isbn: "",
        author: "",
    });
    
</script>

<template>
  <h1>📖 Adicionar Livro</h1>

  <div class="header-btns">
    <button @click="$emit('closeAddBook')" class="btn">
      Fechar x
    </button>
  </div>

  <form class="add-form">

    <div class="form-control">
      <label>Título</label>
      <input
        required
        v-model="newBook.title"
        type="text"
        name="text"
        placeholder="Adicione o título"
      />
    </div>
    <div class="form-control">
      <label>Capa</label>
      <input
        required
        v-model="newBook.cover"
        type="text"
        name="cover"
        placeholder="Adicione o link da imagem de capa"
      />
    </div>
    <div class="form-control">
      <label>Autor</label>
      <input
        required
        v-model="newBook.author"
        type="text"
        name="author"
        placeholder="Adicione o autor"
      />
    </div>
    <div class="form-control">
      <label>ISBN#</label>
      <input
        required
        v-model="newBook.isbn"
        type="text"
        name="isbn"
        placeholder="Adicione o ISBN"
      />
    </div>
    <div class="form-control form-control-check">
      <input
        v-model="newBook.readIt"
        type="checkbox"
        name="readIt"
        id="readIt"
      />
      <label for="readIt">Já li o livro</label>
    </div>

    <button @click.prevent="$emit('saveBook', newBook)" type="submit" class="btn btn-block">Salvar livro</button>
  </form>
</template>

<style scoped>

    input:not([type="checkbox"]) {
        border-color: #dfdfdf;
        background-color: #fdfcfb;
        color: #393939;
        transition: border-color 0.2s ease-in-out;
        font-size: 16px;
        line-height: 22px;
        font-weight: normal;
        font-style: normal;
        height: 50px;
        padding: 0 20px;
        max-width: 100%;
        border-width: 1px;
        border-style: solid;
        appearance: none;
        min-width: 100px;
        width: 100%;
        border-radius: 25px;
        margin: 20px 0 0;
    }
    
    .add-form {
        margin-top: 40px;
    }
    .form-control {
        margin: 20px 0;
    }
    .form-control label {
        display: block;
    }
    
    .form-control-check {
        display: flex;
        align-items: center;
    }
    .form-control-check label {
        flex: 1;
    }
    .form-control-check input {
        flex: 2;
        height: 20px;
    }
    .form-control input[type="checkbox"] {
        width: auto;
        flex: unset;
        height: 20px;
        margin-right: 20px;
    }
    
    input:focus {
        border-color: #484c53;
        outline: none;
    }

    .error {
        color: red;
        font-size: 14px;
        margin-top: 5px;
    }
</style>
