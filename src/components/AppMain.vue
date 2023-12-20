<template>
  <section>
    <div class="card" v-for="(film, index) in films">
      <img :src="getCover(film.poster_path)" :alt="film.title">
      <div class="caption">
        <div class="caption-wrap">
          <p>{{ film.title }}</p>
          <p>{{ film.original_title }}</p>
          <span class="fi">
            <img :src="getFlag(film.original_language)" :alt="`lang: ${film.original_language}`" class="img-rounded">
          </span>
          <span class="rating-stars">
            <img src="../assets/img/star-svgrepo-com.svg" alt="star" v-for="i in getRate(film.vote_average)">
          </span>
          <p>{{ film.overview }}</p>
        </div>
      </div>
    </div>
  </section>
  <section>
    <div class="card" v-for="(serie, index) in series">
      <img :src="getCover(serie.poster_path)" :alt="serie.name">
      <div class="caption">
        <div class="caption-wrap">
          <p>{{ serie.name }}</p>
          <p>{{ serie.original_name }}</p>
          <span class="fi">
            <img :src="getFlag(serie.original_language)" :alt="`lang: ${serie.original_language}`" class="img-rounded">
          </span>
          <span class="rating-stars">
            <img src="../assets/img/star-svgrepo-com.svg" alt="star" v-for="i in getRate(serie.vote_average)">
          </span>
          <p class="overview">{{ serie.overview }}</p>
        </div>
      </div>
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
    getFlag(ref) {
      return `../../node_modules/flag-icons/flags/1x1/${ref}.svg`
    },
    getCover(ref) {
      return `https://image.tmdb.org/t/p/w300/${ref}`
    },
    getRate(num) {
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
@use "../style/partials/mixins" as *;

section {
  @include flex(flex-start, flex-start);
  gap: 1rem;
  overflow-x: auto;
}

.card {
  position: relative;
  &:hover .caption{
    display: block;
  }

  >img {
    display: block;
  }

  .caption {
    position: absolute;
    top: 0;
    left: 0;
    display: none;
    width: 100%;
    height: 100%;
    color: white;
    background-color: rgba(0, 0, 0, 0.365);

    .caption-wrap{
      padding: 2rem;

      .img-rounded {
        border-radius: 50%;
      }
  
      .rating-stars {
        margin: 0 1rem;
  
        img {
          width: 20px;
          margin: 0 .1rem;
        }
      }

      .overview{
        overflow: hidden;
      }
    }
  }
}
</style>