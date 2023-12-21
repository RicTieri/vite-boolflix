<template>
  <main>
    <section>
      <h2>Films</h2>
      <div class="section-wrapper">
        <CardMovie v-for="film in films" :film="film" />
      </div>
    </section>
    <section>
      <h2>Series TV</h2>
      <div class="section-wrapper">
        <CardSerie v-for="serie in series" :serie="serie" />
      </div>
    </section>
  </main>
</template>

<script>
import CardMovie from './CardMovie.vue';
import CardSerie from './CardSerie.vue';

export default {
  data() {
    return {};
  },
  props: {
    films: {
      type: Array,
      required: true
    },
    series: {
      type: Array,
      required: true
    },
  },
  components: {
    CardMovie,
    CardSerie
  }
}
</script>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;

main {
  padding: 1rem 0;
  background-color: rgba(0, 0, 0, 0.74);
  height: calc(100vh - 60px);
  overflow-y: auto;
}

section {
  margin: 0 0 3rem;
  padding: .5rem 1rem;
  background-color: rgba(0, 0, 0, 0.74);
  box-shadow: 0 0 20px 10px rgba(0, 0, 0, 0.463);


  h2 {
    color: white;
  }

  div.section-wrapper {
    @include flex(flex-start, flex-start, row);
    gap: 1rem;
    overflow-x: auto;
    padding: 1rem .75rem;
  }
}
</style>