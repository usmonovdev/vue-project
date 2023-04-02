<template>
  <div class="app">
    <div class="content">
      <AppInfo :moviesLength="movies.length" :viewedMovie="movies.filter(e => e.favourite).length" />
      <div class="search-panel">
        <SearchPanel />
        <AppFilter />
      </div>
      <MovieList :movies="movies" @handleLike="handleLike"/>
      <MovieAdd @createMovie="createMovie"/>
    </div>
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
          like: true,
          id: 1680439521234
        },
        {
          name: "Empire of osman",
          viewers: 632,
          favourite: false,
          like: false,
          id: 1680439523241
        },
        {
          name: "Ertugrul",
          viewers: 745,
          favourite: true,
          like: false,
          id: 1680439524567
        }
      ],
    };
  },
  methods: {
    createMovie(item) {
      this.movies.push(item)
      console.log(item);
    },
    handleLike(e) {
      const arr = this.movies.map(item => {
        if (item.id == e) {
          item.like = !item.like
          console.log(item);
        }
      })
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
