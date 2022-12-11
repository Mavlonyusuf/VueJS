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
    <div class="movie-list items">
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
      movies: [
        {
          name: "Omar",
          viewers: 996,
          like: false,
          favourite: true,
          id: 1,
        },
        {
          name: "Ertugrul",
          viewers: 784,
          like: true,
          favourite: false,
          id: 2,
        },
        {
          name: "Empire of Osman",
          viewers: 885,
          like: true,
          favourite: false,
          id: 3,
        },
      ],
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
  max-height: 16rem;
  box-shadow: 10px 10px 15px rgba(0, 0, 0, 0.15);
}
</style>
