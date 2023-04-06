<template>
  <div class="app">
    <div class="content">
      <AppInfo
        :moviesLength="movies.length"
        :viewedMovie="movies.filter((e) => e.favourite).length"
      />
      <Box class="search-panel">
        <SearchPanel :onHandleUpdateTerm="onHandleUpdateTerm" />
        <AppFilter
          :onHandleUpdateFilter="onHandleUpdateFilter"
          :filterName="filter"
        />
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
import axios from "axios"

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
        
      ],
      term: "",
      filter: "all",
      awesome: true,
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
          return arr;
      }
    },
    onHandleUpdateFilter(e) {
      this.filter = e;
    },
    async fetchData() {
      try {
        const response = await axios.get("https://jsonplaceholder.typicode.com/posts?_limit=10")
        const newArr = response.data.map(data => ({
          name: data.title,
          viewers: data.id * 43,
          favourite: false,
          like: false,
          id: data.id,
        }));
        this.movies = newArr
      } catch (error) {
        console.log(error.message);
      }
    },
    mounted() {
      this.fetchData()
    },
  },
  mounted() {
    this.fetchData()
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
