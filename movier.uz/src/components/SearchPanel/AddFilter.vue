<template>
  <div class="btn-group mt-2">
    <button
      v-for="btn in buttons"
      :key="btn.name"
      @click="updateFilterHandler(btn.name)"
      class="btn btn-outline-dark"
    >
      {{ btn.text }}
    </button>
  </div>
</template>
<script>
export default {
  props: {
    updateFilterHandler: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      filter: "all",
      buttons: [
        {
          name: "all",
          text: "Barcha kinolar",
        },
        {
          name: "popular",
          text: "Mashhur kinolar",
        },
        {
          name: "most",
          text: "Eng ko'p ko'rilgan kinolar",
        },
      ],
    };
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter;
      this.updateFilterHandler(this.filter);
    },
  },
};
</script>
<style scoped>
.btn {
  background-color: white;
  border: 1px solid blueviolet;
  border-radius: 0.6rem;
  color: blueviolet;
}
.btn:focus {
  background-color: black;
  color: white;
  border-color: transparent;
}
.active {
  background-color: black;
  color: white;
  border-color: transparent;
}
</style>
