<template>
  <ul class="list-group">
    <MovieListItem
      v-for="movie in movies"
      :movie="movie"
      :key="movie.id"
      @onLike="$emit('onLike', movie.id)"
      @onFavourite="$emit('onFavourite', movie.id)"
      @onRemove="$emit('onRemove', movie.id)"
    />
  </ul>
</template>
<script>
import MovieListItem from "./MovieListItem.vue";
export default {
  components: {
    MovieListItem,
  },
  props: {
    movies: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {};
  },
  methods: {},
};
</script>
<style scoped></style>
