<template>
  <div id="app">
    <Header />
    <filter-tiles />
  </div>
</template>

<script>
import Header from "./header.vue";
import FilterTiles from "./filter-tiles.vue";

export default {
  name: "App",
  components: {
    Header,
    FilterTiles
  }
};
</script>
<style lang="scss">
@import "./SCSS-variables/styles.scss";
</style>
