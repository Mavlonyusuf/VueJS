<template>
  <div class="add-movies">
    <h3>Yangi kino qo'shish</h3>
    <form class="form-group" @submit.prevent>
      <input
        v-model="name"
        type="text"
        class="form-control"
        placeholder="Qanday kino ?"
        aria-label="Sizing example input"
        aria-describedby="inputGroup-sizing-sm"
      />
      <input
        v-model="viewers"
        type="number"
        class="form-control"
        placeholder="Necha marta ko'rilgan ?"
        aria-label="Sizing example input"
        aria-describedby="inputGroup-sizing-sm"
      />
      <button class="btn btn-primary" type="submit" @click="addMovie">Qo'shish</button>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name: "",
      viewers: "",
      id: 1000,
    };
  },
  methods: {
    addMovie() {
      const movie = {
        name: this.name,
        viewers: this.viewers,
        like: false,
        favourite: false,
        id: this.id++,
      };
      (this.name = ""), (this.viewers = "");
      this.$emit("createMovie", movie);
    },
  },
};
</script>
<style scoped>
::placeholder {
  color: blueviolet;
}
.form-group {
  display: flex;
  flex: 1 1 auto;
}
.form-control {
  margin-right: 0.5rem;
}
</style>
