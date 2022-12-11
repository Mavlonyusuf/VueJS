<template>
  <div>
    <input
      @input="searchValue"
      v-model="term"
      type="text"
      class="form-control"
      placeholder="Kinolarni qidirish"
      aria-describedby="basic-addon1"
    />
  </div>
</template>
<script>
export default {
  props: {},
  data() {
    return {
      term: "",
    };
  },
  methods: {
    searchValue() {
      this.$emit("searchValue", this.term);
    },
  },
};
</script>
<style scoped>
.form-control {
  padding: 1rem 0.5rem;
}
::placeholder {
  color: blueviolet;
}
</style>
