<template>
  <header>
    <h1>BoolFlix</h1>
    <div>
      <input type="text" v-model="searchInput" id="searchBar" name="searchBar" @keyup.enter="doSearch">
      <button @click="doSearch">search</button>
    </div>
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
@use "../style/partials/mixins" as *;

header{
  @include flex(space-between, center)
}
  
</style>