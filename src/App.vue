<template>
  <div id="app">
    <Header />
    <div v-if="filter" class="tile keywords">
      <div v-if="showFilterDashboard" class="filters">
        <div v-if="!removeRoleClicked && role">
          <h4>{{ role }}</h4>
          <div @click="handleRole">&#10006;</div>
        </div>
        <div v-if="!removeLevelClicked && level">
          <h4>{{ level }}</h4>
          <div @click="handleLevel">&#10006;</div>
        </div>
        <div v-if="!removeLanguageClicked && language">
          <h4>{{ language }}</h4>
          <div @click="handleLanguage">&#10006;</div>
        </div>
        <div v-if="!removeToolClicked && tool">
          <h4>{{ tool }}</h4>
          <div @click="handleTool">&#10006;</div>
        </div>
      </div>
      <h5 @click="removeFilterDashboard">Clear</h5>
    </div>
    <div class="tile" v-for="tile in handleShowTiles" :key="tile.data">
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
          <h4 @click="handleLanguageFilter">{{ lang }}</h4>
        </div>
        <div v-for="tool in tile.tools" :key="tool.tools">
          <h4 @click="handleToolFilter">{{ tool }}</h4>
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
      removeRoleClicked: false,
      removeLevelClicked: false,
      removeLanguageClicked: false,
      removeToolClicked: false,
      role: "",
      level: "",
      language: "",
      tool: ""
    };
  },
  computed: {
    handleShowTiles() {
      if (this.filter) {
        if (this.role) {
          return this.data.filter(x => x.role === this.role);
        }
        if (this.level) {
          return this.data.filter(x => x.level === this.level);
        }
        if (this.language) {
          const arr = this.data.filter(x => typeof x.languages === "object");
          return arr.filter(x =>
            x.languages.some(x => x.includes(this.language))
          );
        }
        if (this.tool) {
          const arr = this.data.filter(x => typeof x.tools === "object");
          return arr.filter(x => x.tools.some(x => x.includes(this.tool)));
        }
      }
      return this.data;
    }
  },
  methods: {
    removeFilterDashboard() {
      this.role = "";
      this.level = "";
      this.language = "";
      this.tool = "";
      this.filter = false;
    },
    handleRole() {
      this.removeRoleClicked = true;
      if (
        this.removeLevelClicked &&
        this.removeLanguageClicked &&
        this.removeToolClicked
      ) {
        this.removeFilterDashboard();
      }
    },
    handleLevel() {
      this.removeLevelClicked = true;
      if (
        this.removeRoleClicked &&
        this.removeLanguageClicked &&
        this.removeToolClicked
      ) {
        this.removeFilterDashboard();
      }
    },
    handleLanguage() {
      this.removeLanguageClicked = true;
      if (
        this.removeRoleClicked &&
        this.removeLevelClicked &&
        this.removeToolClicked
      ) {
        this.removeFilterDashboard();
      }
    },
    handleTool() {
      this.removeToolClicked = true;
      if (
        this.removeRoleClicked &&
        this.removeLevelClicked &&
        this.removeLanguageClicked
      ) {
        this.removeFilterDashboard();
      }
    },
    handleRoleFilter() {
      this.role = event.target.innerHTML;
      this.removeRoleClicked = false;
      this.filter = true;
    },
    handleLevelFilter() {
      this.level = event.target.innerHTML;
      this.removeLevelClicked = false;
      this.filter = true;
    },
    handleLanguageFilter() {
      this.language = event.target.innerHTML;
      this.removeLanguageClicked = false;
      this.filter = true;
    },
    handleToolFilter() {
      this.tool = event.target.innerHTML;
      this.removeToolClicked = false;
      this.filter = true;
    }
  }
};
</script>
<style lang="scss">
@import "./SCSS-variables/styles.scss";
</style>
