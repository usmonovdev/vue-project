<template>
  <InputForm
    class="search-input"
    placeholder="Filmlarni qidirish"
    v-model="term"
    @input="onChangeHandler"
  />
</template>

<script>
export default {
  props: {
    onHandleUpdateTerm: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      term: ''
    }
  },
  methods: {
    onChangeHandler(e) {
      this.term = e.target.value
      this.onHandleUpdateTerm(this.term)
    }
  }
};
</script>

<style scoped>
.search-input {
  margin-bottom: 1rem;
  padding: 1.5rem;
  background: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
