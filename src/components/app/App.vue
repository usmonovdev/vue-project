<template>
  <div class="app">
    <div class="content">
      <AppInfo
        :moviesLength="movies.length"
        :viewedMovie="movies.filter((e) => e.favourite).length"
      />
      <Box class="search-panel">
        <SearchPanel :onHandleUpdateTerm="onHandleUpdateTerm" />
        <AppFilter :onHandleUpdateFilter="onHandleUpdateFilter" :filterName="filter"/>
      </Box>
      <MovieList
        :movies="onHandleFilter(onHandleSearch(movies, term), filter)"
        @onToggle="onHandleToggle"
        @onDelete="onHandleDelete"
      />
      <MovieAdd @createMovie="createMovie" />
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
    MovieAdd,
  },
  data() {
    return {
      movies: [
        {
          name: "Omar",
          viewers: 811,
          favourite: false,
          like: true,
          id: 1680439521234,
        },
        {
          name: "Empire of osman",
          viewers: 632,
          favourite: false,
          like: false,
          id: 1680439523241,
        },
        {
          name: "Ertugrul",
          viewers: 745,
          favourite: true,
          like: false,
          id: 1680439524567,
        },
      ],
      term: "",
      filter: "all",
    };
  },
  methods: {
    createMovie(item) {
      this.movies.push(item);
    },
    onHandleToggle({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id == id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
    onHandleDelete(e) {
      this.movies = this.movies.filter((c) => c.id !== e);
    },
    onHandleSearch(arr, term) {
      if (term.length == 0) {
        return arr;
      }

      return arr.filter((c) => c.name.toLowerCase().indexOf(term) > -1);
    },
    onHandleUpdateTerm(e) {
      this.term = e;
    },
    onHandleFilter(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter((c) => c.like);
        case "mostViewers":
          return arr.filter((c) => c.viewers > 500);
        default:
          return arr
      }
    },
    onHandleUpdateFilter(e) {
      this.filter = e
    }
  },
};
</script>

<style>
.app {
  width: 100%;
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
}
</style>
