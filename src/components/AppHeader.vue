<template>
  <header>
    <h1>BoolFlix</h1>
    <input type="text" v-model="searchInput" id="searchBar" name="searchBar" @keyup.enter="doSearch">
    <button @click="doSearch">search</button>
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
    doSearch(){
      this.$emit('search', this.searchInput)
    }
  },
}
</script>

<style lang="scss">
  
</style>