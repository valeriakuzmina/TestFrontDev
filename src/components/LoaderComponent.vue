<template>
  <div v-if="loading" class="loader">
    Loading...
  </div>
</template>

<script>
export default {
  name: 'LoaderComponent.vue',
  props: {
    loading: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style scoped>
.loader {
  font-size: 20px;
  color: #333;
}
</style>
