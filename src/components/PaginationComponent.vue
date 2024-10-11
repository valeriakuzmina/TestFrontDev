<template>
  <div class="pagination">
    <button 
      @click="changePage(currentPage - 1)" 
      :disabled="currentPage === 1"
    >
      &lt; <!-- Или можно использовать изображение для стрелки назад -->
    </button>

    <span v-for="page in totalPages" :key="page" class="page-number">
      <button 
        @click="changePage(page)" 
        :class="{ active: page === currentPage }"
      >
        {{ page }}
      </button>
    </span>

    <button 
      @click="changePage(currentPage + 1)" 
      :disabled="currentPage === totalPages"
    >
      &gt; <!-- Или можно использовать изображение для стрелки вперед -->
    </button>
  </div>
</template>

<script>
export default {
  name: "PaginationComponent",
  props: ['currentPage', 'totalPages'],
  methods: {
    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.$emit('changePage', this.$props.query, page);
      }
    }
  }
}
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
  margin-bottom: 20px;
}

.page-number {
  margin: 0 5px;
}

button {
  margin: 0 3px;
  padding: 5px 10px;
  font-size: 14px;
  cursor: pointer;
  background: none;
  border: none;
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.active {
  font-weight: bold;
  text-decoration: underline;
}
</style>
