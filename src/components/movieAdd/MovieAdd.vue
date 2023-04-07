<template>
  <Box class="movie-add-form">
    <h3>Yangi film qo'shish</h3>
    <form class="add-form d-flex" @submit.prevent>
      <InputForm
        class="new-movie-label"
        placeholder="Film nomi"
        v-model="name"
      />
      <InputForm
        type="number"
        class="form-control new-movie-label"
        placeholder="Necha marotaba ko'rilgan?"
        v-model="viewers"
      />
      <PrimaryButton
        class="btn btn-outline-dark"
        type="submit"
        @click="addMovie"
        >Qo'shish</PrimaryButton
      >
    </form>
  </Box>
</template>
<script>
export default {
  data() {
    return {
      name: "",
      viewers: "",
    };
  },
  methods: {
    addMovie() {
      if (!this.name || !this.viewers) return;
      const newMovie = {
        name: this.name,
        viewers: this.viewers,
        favourite: false,
        like: false,
      };
      this.$emit("createMovie", newMovie);
    },
  },
};
</script>
<style>
.movie-add-form {
  margin-top: 1.5rem;
}
</style>
