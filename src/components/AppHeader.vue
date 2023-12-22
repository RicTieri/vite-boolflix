<template>
  <header>
    <h1>BoolFlix</h1>
    <nav>
      <input type="text" v-model="searchInput" id="searchBar" name="searchBar" @keyup.enter="doSearch">
      <button id="searchBtn" @click="doSearch">search</button>
    </nav>
  </header>
</template>

<script>
export default {
  data() {
    return {
      searchInput: ''
    }
  },
  methods: {
    doSearch() {
      this.$emit('search', this.searchInput)
    }
  },
}
</script>

<style lang="scss">
@use "../style/partials/mixins" as *;

header {
  @include flex(space-between, center);
  padding: 0 1rem;
  height: 60px;
  background-color: rgba(0, 0, 0, 0.84);
  box-shadow: 0 0 20px 10px rgba(0, 0, 0, 0.235);
  box-shadow: inset 0 0 20px 10px rgba(0, 0, 0, 0.235);

  h1 {
    color: red;
  }

  nav {
    #searchBar {
      background-color: transparent;
      color: white;
      box-shadow: 0 0 20px 10px rgba(0, 0, 0, 0.235);
      border: 1px solid rgba(128, 128, 128, 0.507);
      border-radius: 10px;
      padding: .25rem .5rem;
      margin-right: 1rem;
    }

    #searchBtn {
      color: rgba(255, 255, 255, 0.559);
      border: none;
      background-color: transparent;

      &:hover {
        color: rgba(255, 255, 255, 0.959);
        scale: 1.2;
        cursor: pointer;
      }
    }
  }
}
</style>