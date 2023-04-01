<template>
  <div class="app-info">
    <p class="fs-3 text-uppercase">Barcha filmlar soni: {{ moviesLength }}</p>
    <p class="fs-3 text-uppercase">Ko'rilgan filmlar soni: {{ viewedMovie }}</p>
  </div>
</template>

<script>
  export default {
    props: {
      moviesLength: {
        type: Number,
        required: true,
      },
      viewedMovie: {
        type: Number,
        required: true
      }
    }
  }
</script>

<style scoped>
  .app-info {
    padding: 1.5rem;
    border-radius: 4px;
    background-color: #fcfaf5;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
  }
</style>
