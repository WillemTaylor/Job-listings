<template>
  <div id="app">
    <Header />
    <div v-if="filter" class="tile keywords">
      <div v-if="showFilterDashboard" class="filters">
        <div v-if="role">
          <h4>{{ role }}</h4>
          <div @click="handleRemoveFilter">&#10006;</div>
        </div>
        <div v-if="level">
          <h4>{{ level }}</h4>
          <div @click="handleRemoveFilter">&#10006;</div>
        </div>
      </div>
      <h5 @click="removeFilterDashboard">Clear</h5>
    </div>
    <div class="tile" v-for="tile in data" :key="tile.data">
      <div class="info-container">
        <div>
          <img :src="require(`${tile.logo}`)" />
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
        <div>
          <h4 @click="handleRoleFilter">{{ tile.role }}</h4>
        </div>
        <div>
          <h4 @click="handleLevelFilter">{{ tile.level }}</h4>
        </div>
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
      data: json,
      filter: false,
      showFilterDashboard: true,
      role: "",
      level: ""
    };
  },
  mounted() {
    if (this.roleFilter === "" && this.levelFilter === "") {
      this.showFilterDashboard = false;
    }
  },
  methods: {
    removeFilterDashboard() {
      this.role = "";
      this.level = "";
      this.filter = false;
    },
    handleRemoveFilter() {
      event.target.parentElement.remove();
    },
    handleRoleFilter() {
      this.role = event.target.innerHTML;
      this.filter = true;
    },
    handleLevelFilter() {
      this.level = event.target.innerHTML;
      this.filter = true;
    }
  }
};
</script>
<style lang="scss">
@import "./SCSS-variables/styles.scss";
</style>
