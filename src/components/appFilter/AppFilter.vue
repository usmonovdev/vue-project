<template>
  <div class="btn-group">
    <button
      v-for="btn in filterButton"
      :key="btn.name"
      class="btn"
      type="button"
      @click="onHandleFilter(btn.name)"
      :class="[filterName === btn.name ? 'btn-dark' : 'btn-outline-dark']"
    >
      {{ btn.title }}
    </button>
  </div>
</template>

<script>
import ButtonFilter from "../button/ButtonFilter.vue";
export default {
  components: {
    ButtonFilter,
  },
  props: {
    onHandleUpdateFilter: {
      type: Function,
      required: true,
    },
    filterName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      filterButton: [
        {
          title: "Barcha filmlar",
          name: "all",
        },
        {
          title: "Mashhur filmlar",
          name: "popular",
        },
        {
          title: "Eng ko'p ko'rilgan filmlar",
          name: "mostViewers",
        },
      ],
      filter: "all",
    };
  },
  methods: {
    onHandleFilter(e) {
      this.filter = e;
      this.onHandleUpdateFilter(this.filter);
    },
  },
};
</script>

<style></style>
