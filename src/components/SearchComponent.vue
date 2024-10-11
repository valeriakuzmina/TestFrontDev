<template>
  <div class="search-bar">
    <input
    class="input-for-search"
      type="text"
      placeholder="Поиск фильмов"
      v-model="query"
      @keyup.enter="search"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: ''
    };
  },
  methods: {
    search() {
      this.$emit("onSearch", this.query);
    }
  }
}
</script>

<style scoped>
.search-bar {
  display: flex;
  align-items: center;
}
input {
    width: 850px;
  padding: 5px;
  font-size: 14px;
  margin-right: 5px;
}
</style>