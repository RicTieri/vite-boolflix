<template>
  <section>
    <div class="card" v-for="(film, index) in films">
      <div>
        <img :src="getCover(film.poster_path)" :alt="film.title">
      </div>
      <h1>{{ index + 1 }}</h1>
      <p>{{ film.title }}</p>
      <p>{{ film.original_title }}</p>
      <span class="fi">
        <img :src="getFlag(film.original_language)" :alt="`lang: ${film.original_language}`" class="img-rounded">
      </span>
      <p>{{ film.original_language }}</p>
      <p>{{ film.vote_average }}</p>
    </div>
  </section>
  <section>
    <div class="card" v-for="(serie, index) in series">
      <div>
        <img :src="getCover(serie.poster_path)" :alt="serie.name">
      </div>
      <h1>{{ index + 1 }}</h1>
      <p>{{ serie.name }}</p>
      <p>{{ serie.original_name }}</p>
      <span class="fi">
        <img :src="getFlag(serie.original_language)" :alt="`lang: ${serie.original_language}`" class="img-rounded">
      </span>
      <p>{{ serie.original_language }}</p>
      <p>{{ serie.vote_average }}</p>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {

    }
  },
  methods: {
    getFlag(ref){
      return `../../node_modules/flag-icons/flags/1x1/${ref}.svg`
    },
    getCover(ref){
      return `https://image.tmdb.org/t/p/w300/${ref}`
    }
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
  }
}
</script>

<style lang="scss">
.img-rounded{
  border-radius: 50%;
}
</style>