<template>
  <div class="content">
    <div v-if="movies.length" class="movie-container-grid">
      <div v-for="movie in movies" :key="movie.imdbID" class="movie-card">
        <img :src="movie.Poster" alt="Movie poster" />
        <p>Name: {{ movie.Title }}</p>
        <p>Year: {{ movie.Year }}</p>
        <p>imdbID: {{ movie.imdbID }}</p>
        <p>Type: {{ movie.Type }}</p>
      </div>
    </div>
    <no-results-component v-if="!movies.length"></no-results-component>
  </div>
</template>

<script>
import NoResultsComponent from "./NoResultsComponent.vue";

export default {
  name: "ContentComponent.vue",
  components: {
    NoResultsComponent,
  },
  props: ["movies"],
};
</script>

<style scoped>
.content {
  margin-top: 40px;
  margin-bottom: 40px;
}

.movie-container-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* 4 колонки */
  grid-template-rows: repeat(2, auto); /* 2 строки */
  gap: 20px; /* Пробел между элементами */
}
.movie-card {
  background-color: white;
  border: 1px solid #ddd;
  padding: 10px;
  text-align: left;
  padding-left: 80px;
}
</style>
