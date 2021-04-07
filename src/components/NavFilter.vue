<template>
  <nav class="nav-filter">
    <button
      class="nav-filter-btn"
      @click="handleFilter('all')"
      :class="{ 'nav-filter-btn--active': currentBy === 'all' }"
    >
      View All
    </button>
    <button
      class="nav-filter-btn"
      @click="handleFilter('completed')"
      :class="{ 'nav-filter-btn--active': currentBy === 'completed' }"
    >
      Completed
    </button>
    <button
      class="nav-filter-btn"
      @click="handleFilter('ongoing')"
      :class="{ 'nav-filter-btn--active': currentBy === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["currentBy"],
  methods: {
    handleFilter(by) {
      this.$emit("filter", by);
    },
  },
};
</script>

<style>
.nav-filter {
    width: 100%;
    margin-bottom: 1rem;
}
.nav-filter-btn {
    border: none;
    color: var(--grey);
    background: none;
    margin-right: 1rem;
    font-weight: bold;
    cursor: pointer;
    outline: none;
}
.nav-filter-btn--active {
    color: var(--darkgrey);
}
</style>