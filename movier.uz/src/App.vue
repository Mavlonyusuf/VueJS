<template>
  <div class="app-vue container">
    <div class="app-info items">
      <AppInfo
        :allCountMovies="movies.length"
        :favouriteMovies="movies.filter((m) => m.favourite).length"
      />
    </div>
    <div class="search-panel items">
      <SearchPanel @searchValue="updateMovie" />
      <AddFilter :updateFilterHandler="updateFilterHandler" />
    </div>
    <div class="items" v-if="!movies.length">
      <div class="spinner-border text-warning" role="status">
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>
    <div class="movie-list items" v-else="movies.length">
      <MovieList
        :movies="filterHandler(searchMovie(movies, this.term), filter)"
        @onLike="onLikeHandler"
        @onFavourite="onFavouriteHandler"
        @onRemove="onDelete"
      />
    </div>
    <div class="movie-add items">
      <MovieAddForm @createMovie="newMovie" :oldCountMovies="movies.length" />
    </div>
  </div>
</template>
<script>
import AppInfo from "./components/AppInfo/AppInfo.vue";
import SearchPanel from "./components/SearchPanel/SearchPanel.vue";
import AddFilter from "./components/SearchPanel/AddFilter.vue";
import MovieList from "./components/MovieList/MovieList.vue";
import MovieListItem from "./components/MovieList/MovieListItem.vue";
import MovieAddForm from "./components/MovieAddForm/MovieAddForm.vue";
export default {
  components: {
    AppInfo,
    SearchPanel,
    AddFilter,
    MovieList,
    MovieListItem,
    MovieAddForm,
  },
  data() {
    return {
      movies: [],
      term: "",
      errorMessage: { name: "ERROR !" },
      filter: "all",
    };
  },
  methods: {
    newMovie(items) {
      this.movies.push(items);
    },
    onLikeHandler(id) {
      const arr = this.movies.map((movie) => {
        if (movie.id == id) {
          movie.like = !movie.like;
        }
      });
    },
    onFavouriteHandler(id) {
      const arr1 = this.movies.map((movie) => {
        if (movie.id == id) {
          movie.favourite = !movie.favourite;
        }
        return movie;
      });
    },
    onDelete(id) {
      this.movies = this.movies.filter((a) => a.id != id);
    },
    searchMovie(arr, term) {
      if (term.length == 0) {
        return arr;
      } else if (term.length != 0) {
        return arr.filter((a) => a.name.toLowerCase().includes(term));
      } else if (arr.length == 0) {
        this.movies = this.movies.push(this.errorMessage);
      }
    },
    updateMovie(item) {
      this.term = item;
    },
    filterHandler(arr, filter) {
      switch (filter) {
        case "most":
          return arr.filter((a) => a.favourite);
          break;
        case "popular":
          return arr.filter((a) => a.like);
          break;
        default:
          return arr;
          break;
      }
    },
    updateFilterHandler(filter) {
      this.filter = filter;
    },
    async fetchMovie() {
      const response = await fetch("https://jsonplaceholder.typicode.com/todos?_limit=10")
        .then((data) => {
          return data.json();
        })
        .then((dataJson) => {
          setTimeout(() => {
            const newArr = dataJson.map((item) => ({
              id: item.id,
              name: item.title,
              like: item.completed,
              viewers: item.id * 105,
              favourite: false,
            }));
            this.movies = newArr;
          }, 1500);
        })
        .catch(() => {
          alert("Serverda xatolik mavjud !!!");
        });
    },
  },
  mounted() {
    this.fetchMovie();
  },
};
</script>
<style>
@import url(https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200;300;400;500;600;800;900&display=swap);

body {
  font-family: "Montserrat", sans-serif;
  color: blueviolet;
}
.app-vue {
  position: relative;
  height: 100%;
  text-align: center;
}
.items {
  border-radius: 0.5rem;
  background-color: rgb(241, 235, 235);
  padding: 1rem 2rem;
  margin: 5rem 15rem;
  height: 100%;
  box-shadow: 10px 10px 15px rgba(0, 0, 0, 0.15);
}
</style>
