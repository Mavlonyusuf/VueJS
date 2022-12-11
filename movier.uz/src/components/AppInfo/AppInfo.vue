<template>
  <div>
    <h1>Barcha Kinolar Soni : {{ allCountMovies }}</h1>
    <h2>Sevimli Film : {{ favouriteMovies }}</h2>
  </div>
</template>
<script>
export default {
  props: {
    allCountMovies: {
      type: Number,
      required: true,
    },
    favouriteMovies: {
      type: Number,
      required: true,
    },
  },
};
</script>
<style></style>
