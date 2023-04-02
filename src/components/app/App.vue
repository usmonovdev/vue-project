<template>
  <div class="app">
    <div class="content">
      <AppInfo :moviesLength="movies.length" :viewedMovie="movies.filter(e => e.favourite).length" />
      <div class="search-panel">
        <SearchPanel />
        <AppFilter />
      </div>
      <MovieList :movies="movies"/>
      <MovieAdd @createMovie="createMovie"/>
    </div>
    <button @click="handleconsole">click</button>
  </div>
</template>

<script>
import AppInfo from "../appInfo/AppInfo.vue";
import SearchPanel from "../searchPanel/SearchPanel.vue";
import AppFilter from "../appFilter/AppFilter.vue";
import MovieList from "../movieList/MovieList.vue";
import MovieAdd from "../movieAdd/MovieAdd.vue";

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAdd
  },
  data() {
    return {
      movies: [
        {
          name: "Omar",
          viewers: 811,
          favourite: false,
          like: true
        },
        {
          name: "Empire of osman",
          viewers: 632,
          favourite: false,
          like: false
        },
        {
          name: "Ertugrul",
          viewers: 745,
          favourite: true,
          like: false
        }
      ],
    };
  },
  methods: {
    createMovie(item) {
      this.movies.push(item)
      console.log(item);
    }
  }
};
</script>

<style>
.app {
  width: 100vw;
  height: 100vh;
  color: #000;
}
.content {
  width: 60vw;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}
.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
