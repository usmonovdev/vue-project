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
      <Box
        v-if="!movies.length && !isLoading"
        class="d-flex justify-content-center"
        >No Items!</Box
      >
      <Box v-else-if="isLoading" class="d-flex justify-content-center"
        ><Loader
      /></Box>
      <MovieList
        v-else="movies.length"
        :movies="onHandleFilter(onHandleSearch(movies, term), filter)"
        @onToggle="onHandleToggle"
        @onDelete="onHandleDelete"
      />
      <Box class="d-flex justify-content-center" v-if="!isLoading">
        <nav aria-label="pagination">
          <ul class="pagination pagination-sm">
            <li
              v-for="pageNumber in totalPages"
              class="page-item"
              :class="{ active: pageNumber === page }"
              @click="onChangePage(pageNumber)"
            >
              <span class="page-link">{{ pageNumber }}</span>
            </li>
          </ul>
        </nav>
      </Box>
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
import axios from "axios";

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
      movies: [],
      term: "",
      filter: "all",
      awesome: true,
      isLoading: false,
      limit: 10,
      page: 1,
      totalPages: 100,
    };
  },
  methods: {
    async createMovie(item) {
      try {
        const response = await axios.post("https://jsonplaceholder.typicode.com/posts", item)
        this.movies.push(response.data);
      } catch (error) {
        alert(error.message)
      }
    },
    onHandleToggle({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id == id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
    async onHandleDelete(e) {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/posts/${e}`)
        this.movies = this.movies.filter((c) => c.id !== e);
      } catch (error) {
        alert(error.message)
      }
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
        this.isLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _limit: this.limit,
              _page: this.page,
            },
          }
        );
        const newArr = response.data.map((data) => ({
          name: data.title,
          viewers: data.id * 43,
          favourite: false,
          like: false,
          id: data.id,
        }));
        this.totalPages = Math.ceil(
          response.headers["x-total-count"] / this.limit
        );
        this.movies = newArr;
      } catch (error) {
        alert(error.message)
      } finally {
        this.isLoading = false;
      }
    },
    onChangePage(e) {
      this.page = e
    },
  },
  mounted() {
    this.fetchData();
  },
  watch: {
    page() {
      this.fetchData()
    }
  }
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
