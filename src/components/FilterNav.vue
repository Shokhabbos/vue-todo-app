<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')"
         :class="{ active: current === 'all' }">
      ALL
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >
      COMPLETED
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      ONGOING
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    updateFilter(by) {
      this.$emit("filterChange", by);
    },
  },
};
</script>

<style>
.filter-nav{
  margin-top: 15px;
}
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  font-size: 12px;
  outline: none;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active{
    color: #555;
}
</style>