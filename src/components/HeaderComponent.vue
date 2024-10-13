<template>
  <div>
    <header class="header">
      <h1 class="logo">Movie Catalog</h1>
      <search-component @onSearch="onSearch"></search-component>
      <div class="user">
        <img src="/images/user.png" alt="photo" aria-placeholder="photo-user" class="icon-user">
        <p class="user-name">Alexsander Borisenko</p>
        <img src="/images/arrow.png" alt="photo-arrow" class="arrow">
      </div>
    </header>
  </div>
</template>

<script>
import SearchComponent from './SearchComponent.vue';

export default {
  name: 'HeaderComponent',
  components: {
    SearchComponent
  },
  props: {
    onSearch: {
      type: Function,
      required: true
    }
  },
}
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #333;
  color: white;
  padding-left: 50px;
  margin: 0 auto;
  background-color: rgb(92, 168, 219);
}

.logo {
  color: #333;
}

.user {
  display: flex;
  align-items: center;
  justify-content: center;
  padding-right: 50px;
}

.user-name {
  font-size: 16px;
  color: #333;
  font-weight: 700;
}

.icon-user {
  width: 45px;
  height: 45px;
}

.arrow {
  width: 45px;
  height: 45px;
}
</style>
