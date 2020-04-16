<template>
  <div id="app">
    <Header />
    <div class="tile">
      <div class="info-container">
        <div>
          <img src="./images/photosnap.svg" />
        </div>
        <div>
          <h4>Photosnap</h4>
          <div class="new-tag">
            <p>NEW!</p>
          </div>
          <div class="featured-tag">
            <p>FEATURED</p>
          </div>
          <h3>Senior Frontend Developer</h3>
          <p>1d ago &bull; Full Time &bull; USA Only</p>
          <hr class="desktop-hide" />
        </div>
      </div>
      <div class="filters">
        <h4>role</h4>
        <h4>level</h4>
        <h4>languages</h4>
        <h4>tools</h4>
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
