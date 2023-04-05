<template>
  <Box>
    <p class="fs-3 text-uppercase">Barcha filmlar soni: {{ moviesLength }}</p>
    <p class="fs-3 text-uppercase">Ko'rilgan filmlar soni: {{ viewedMovie }}</p>
  </Box>
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

<style scoped></style>
