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
      <span class="rating-stars">
        <img src="../assets/img/star-svgrepo-com.svg" alt="star"  v-for="i in getRate(film.vote_average)">
      </span>
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
      <span class="rating-stars">
        <img src="../assets/img/star-svgrepo-com.svg" alt="star"  v-for="i in getRate(serie.vote_average)">
      </span>
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
    },
    getRate(num){
      return Math.round(num / 2)
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

<style lang="scss" scoped>
.img-rounded{
  border-radius: 50%;
}

.rating-stars{
  margin: 0 1rem;
  img{
    width: 20px;
    margin: 0 .1rem;
  }
}
</style>