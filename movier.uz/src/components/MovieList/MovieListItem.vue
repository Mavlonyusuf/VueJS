<template>
  <li
    class="list-group-item"
    :class="[{ like: movie.like }, { favourite: movie.favourite }]"
  >
    <div class="title" @click="onLike">{{ movie.name }}</div>
    <div class="list-icons">
      <input type="number" :value="movie.viewers" />
      <span class="icons">
        <button type="button" @click="onFavourite"><i class="fas fa-cookie"></i></button>
        <button type="button" @click="onRemove"><i class="fas fa-trash"></i></button>
        <i class="fas fa-star"></i>
      </span>
    </div>
  </li>
</template>
<script>
export default {
  props: {
    movie: {
      type: Object,
      requiered: true,
    },
  },
  data() {
    return {};
  },
  methods: {
    onLike() {
      this.$emit("onLike", this.movie.id);
    },
    onFavourite() {
      this.$emit("onFavourite", this.movie.id);
    },
    onRemove() {
      this.$emit("onRemove", this.movie.id);
    },
  },
};
</script>
<style scoped>
.list-group-item {
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  color: blueviolet;
  border: 0;
  margin-bottom: 5px;
  border-radius: 0;
  border-bottom: 1px solid rgb(152, 148, 148);
  background-color: transparent;
}
.list-group-item:last-child {
  border: 0;
  padding-bottom: 0;
}
.list-icons {
  width: 40%;
  display: flex;
  justify-content: space-between;
}
.list-icons input {
  background-color: transparent;
  border: 0;
  outline: none;
}
.icons button {
  border: 0;
  background-color: transparent;
}
.list-group-item.favourite .title,
.list-group-item.favourite input,
.list-group-item.favourite .fa-cookie {
  transition: 0.5s all;
  color: orange;
}
.list-group-item.like .fa-star {
  opacity: 1;
  transition: 0.5s all;
  transform: translateX(0);
}
.fa-star {
  color: orange;
  transition: 0.5s all;
  transform: translateX(30px);
  opacity: 0;
}
.fa-trash {
  color: red;
  margin-right: 6px;
}
</style>
