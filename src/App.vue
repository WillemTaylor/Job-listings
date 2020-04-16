<template>
  <div id="app">
    <Header />
    <div class="tile" v-for="tile in data" :key="tile.data">
      <div class="info-container">
        <div>
          <img src="./images/photosnap.svg" />
        </div>
        <div>
          <h4>{{ tile.company }}</h4>
          <div v-if="tile.new" class="new-tag">
            <p>NEW!</p>
          </div>
          <div v-if="tile.featured" class="featured-tag">
            <p>FEATURED</p>
          </div>
          <h3>{{ tile.position }}</h3>
          <p>
            {{ tile.postedAt }} &bull; {{ tile.contract }} &bull;
            {{ tile.location }}
          </p>
          <hr class="desktop-hide" />
        </div>
      </div>
      <div class="filters">
        <h4>{{ tile.role }}</h4>
        <h4>{{ tile.level }}</h4>
        <div v-for="lang in tile.languages" :key="lang.languages">
          <h4>{{ lang }}</h4>
        </div>
        <div v-for="tool in tile.tools" :key="tool.tools">
          <h4>{{ tool }}</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/header.vue";
import json from "../data.json";

export default {
  name: "App",
  components: {
    Header
  },
  data() {
    return {
      data: json
    };
  }
};
</script>
<style lang="scss">
@import "./SCSS-variables/styles.scss";
</style>
