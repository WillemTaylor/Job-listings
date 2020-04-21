<template>
  <div>
    <div v-if="filter" class="keywords">
      <div class="filters">
        <div v-if="!removeClicked && role">
          <h4>{{ role }}</h4>
          <div id="role" @click="handleRemoveFilter">&#10006;</div>
        </div>
        <div v-if="!removeClicked && level">
          <h4>{{ level }}</h4>
          <div id="level" @click="handleRemoveFilter">&#10006;</div>
        </div>
        <div v-if="!removeClicked && language">
          <h4>{{ language }}</h4>
          <div id="language" @click="handleRemoveFilter">&#10006;</div>
        </div>
        <div v-if="!removeClicked && tool">
          <h4>{{ tool }}</h4>
          <div id="tool" @click="handleRemoveFilter">&#10006;</div>
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
          <h4 id="role" @click="handleClickFilter">{{ tile.role }}</h4>
        </div>
        <div>
          <h4 id="level" @click="handleClickFilter">{{ tile.level }}</h4>
        </div>
        <div v-for="lang in tile.languages" :key="lang.languages">
          <h4 id="language" @click="handleClickFilter">{{ lang }}</h4>
        </div>
        <div v-for="tool in tile.tools" :key="tool.tools">
          <h4 id="tool" @click="handleClickFilter">{{ tool }}</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import json from "../data.json";

export default {
  name: "FilterTiles",
  data() {
    return {
      data: json,
      filter: false,
      removeClicked: false,
      role: "",
      level: "",
      language: "",
      tool: ""
    };
  },
  computed: {
    handleShowTiles() {
      let role = this.role;
      let level = this.level;
      let language = this.language;
      let tool = this.tool;

      if (role || level || language || tool) {
        return this.data
          .filter(arr => (role.length > 0 ? arr.role === role : arr))
          .filter(arr => (level.length > 0 ? arr.level === level : arr))
          .filter(arr => (language ? typeof arr.languages === "object" : arr))
          .filter(arr =>
            language.length > 0
              ? arr.languages.some(x => x.includes(language))
              : arr
          )
          .filter(arr => (tool ? typeof arr.tools === "object" : arr))
          .filter(arr =>
            tool.length > 0 ? arr.tools.some(x => x.includes(tool)) : arr
          );
      } else return this.removeFilterDashboard();
    }
  },
  methods: {
    removeFilterDashboard() {
      this.role = "";
      this.level = "";
      this.language = "";
      this.tool = "";
      this.filter = false;
      return this.data;
    },
    handleRemoveFilter() {
      let id = event.target.id;

      id === "role"
        ? (this.role = "")
        : id === "level"
        ? (this.level = "")
        : id === "language"
        ? (this.language = "")
        : id === "tool"
        ? (this.tool = "")
        : "";
      this.handleShowTiles;
    },
    handleClickFilter() {
      let result = event.target.innerHTML;
      let id = event.target.id;

      id === "role"
        ? (this.role = result)
        : id === "level"
        ? (this.level = result)
        : id === "language"
        ? (this.language = result)
        : id === "tool"
        ? (this.tool = result)
        : "";
      this.removeClicked = false;
      this.filter = true;
    }
  }
};
</script>
