<template>
  <div>
    <h3>Agregar Libro</h3>
    <div v-if="!submitted">
      <div class="mb-3">
        <label for="isbn" class="form-label">ISBN</label>
        <input
          type="text"
          class="form-control"
          id="isbn"
          required
          name="isbn"
          v-model="book.isbn"
        />
      </div>
      <div class="mb-3">
        <label for="title" class="form-label">Titulo</label>
        <input
          type="text"
          class="form-control"
          id="title"
          required
          name="title"
          v-model="book.title"
        />
      </div>
      <div class="mb-3">
        <label for="author" class="form-label">Autor</label>
        <input
          type="text"
          class="form-control"
          id="author"
          required
          name="author"
          v-model="book.author"
        />
      </div>
      <div class="mb-3">
        <label for="editorial" class="form-label">Editorial</label>
        <input
          type="text"
          class="form-control"
          id="editorial"
          required
          name="editorial"
          v-model="book.editorial"
        />
      </div>
      <div class="mb-3">
        <label for="page_number" class="form-label">Numero de Paginas</label>
        <input
          type="number"
          class="form-control"
          id="page_number"
          required
          name="page_number"
          v-model="book.page_number"
        />
      </div>
      <div class="mb-3">
        <button @click="saveBook" class="btn btn-primary me-3">Guardar</button>
        <button @click="$router.push({ name: 'books' })" class="btn btn-danger">
          Volver
        </button>
      </div>
    </div>
    <div v-else>
      <div class="alert alert-success" role="alert">
        Libro Guardado Exitosamente!
      </div>
      <button @click="newBook" class="btn btn-primary">
        Agregar Nuevo Libro
      </button>
    </div>
  </div>
</template>

<script>
import BookDataService from "../services/BookDataService";

export default {
  name: "add-book",
  data() {
    return {
      book: {
        id: null,
        isbn: "",
        title: "",
        author: "",
        editorial: "",
        page_number: 0,
      },
      submitted: false,
    };
  },
  methods: {
    saveBook() {
      var data = {
        isbn: this.book.isbn,
        title: this.book.title,
        author: this.book.author,
        editorial: this.book.editorial,
        page_number: this.book.page_number,
      };
      BookDataService.create(data)
        .then((response) => {
          this.book.id = response.data.id;
          alert(response.data);
          this.$router.push({ name: "books" });
        })
        .catch((e) => {
          alert(e.response.data);
        });
    },
    newBook() {
      this.submitted = false;
      this.book = {};
    },
  },
};
</script>