<template>
  
  <div class="card" v-for="film in films">
    <p>{{ film.title }}</p>
    <p>{{ film.original_title }}</p>
    <p>{{ film.original_language }}</p>
    <p>{{ film.vote_average }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  props: {
    films: {
      type: Array,
      required: true
    }
  }
}
</script>

<style lang="scss"></style>