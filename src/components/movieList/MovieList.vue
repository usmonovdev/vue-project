<template>
  <ul class="movie-list list-group">
    <MovieItems />
    <MovieItems />
    <MovieItems />
  </ul>
</template>

<script>
import MovieItems from "../movieItems/MovieItems.vue";

export default { components: { MovieItems } };
</script>

<style scoped>
.movie-list {
  margin-top: 1rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
