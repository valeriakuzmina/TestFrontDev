<template>
  <div id="app">
    <header-component :onSearch="fetchMovies"></header-component>
    <loader-component :loading="loading"></loader-component>
    <div v-if="searchMessage" class="search-message">{{ searchMessage }}</div>
    <content-component :movies="movies"></content-component>
    <pagination-component
      :currentPage="currentPage"
      @changePage="fetchMovies"
      :totalPages="totalPages"
    ></pagination-component>
  </div>
</template>

<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import ContentComponent from "./components/ContentComponent.vue";
import LoaderComponent from "./components/LoaderComponent.vue";
import PaginationComponent from "./components/PaginationComponent.vue";

export default {
  name: "App",
  components: {
    "header-component": HeaderComponent,
    "content-component": ContentComponent,
    "loader-component": LoaderComponent,
    "pagination-component": PaginationComponent,
  },
  data() {
    return {
      movies: [],
      loading: false,
      currentPage: 1,
      query: "", // Инициализация пустого значения для поискового запроса
      totalMovies: 0,
      searchMessage: "",
    };
  },

  mounted() {
    // Загружаем фильмы без параметров при загрузке компонента
    this.fetchMovies(""); // передаем пустую строку для начальной загрузки
  },

  methods: {
    async fetchMovies(query = "", page = 1) {
      this.loading = true;
      this.query = query || this.query;
      this.currentPage = page;

      try {
        const response = await fetch(
          `https://www.omdbapi.com/?apikey=8523cbb8&s=${this.query}&page=${this.currentPage}`
        );
        const data = await response.json();

        // Обработка данных ответа
        if (data.Response === "True") {
          // Сохраняем все найденные фильмы
          this.movies = data.Search || [];
          this.movies = this.movies.slice(0, 8);
          this.totalMovies = parseInt(data.totalResults);
          this.searchMessage = `You searched for: "${this.query}". Found ${this.totalMovies} movies.`; // Устанавливаем сообщение
          const totalResults = data.totalResults
            ? parseInt(data.totalResults)
            : 0;
          this.totalPages = Math.min(Math.ceil(totalResults / 12), 10);
          // Обновляем общее количество страниц, деля общее количество результатов на 12
          // this.totalPages = Math.ceil(data.totalResults / 12); // totalResults - общее количество результатов от API
        } else {
          this.movies = [];
          this.searchMessage = "";
          this.totalPages = 0; // Обнуляем, если фильмы не найдены
          console.error("No movies found:", data.Error);
        }
      } catch (error) {
        console.error("Error fetching movies:", error);
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.search-message{
  margin-top: 30px;
  font-size: 24px;
  font-weight: 700;
  text-align: left;
  margin-left: 100px;
}
</style>
