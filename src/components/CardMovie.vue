<template>
  <article class="card">
    <img :src="getCover(film.poster_path)" :alt="film.title">
    <div class="caption">
      <div class="caption-wrap">
        <h3>{{ film.title }}</h3>
        <h5 v-if="film.title !== film.original_title">{{ film.original_title }}</h5>
        <span class="fi">
          <img :src="getFlag(film.original_language)" :alt="`lang: ${film.original_language}`" class="img-rounded">
        </span>
        <span class="rating-stars">
          <img src="../assets/img/star-svgrepo-com.svg" alt="star" v-for="i in getRate(film.vote_average)">
        </span>
        <p class="overview">{{ getOverview(film.overview) }}</p>
        <span @click="$emit('info_pop', film)">info</span>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  props: {
    film: {
      type: Object,
      required: true
    }
  },
  methods: {
    getFlag(ref) {
      return `../../node_modules/flag-icons/flags/1x1/${ref}.svg`;
    },
    getCover(ref) {
      return `https://image.tmdb.org/t/p/w342/${ref}`;
    },
    getRate(num) {
      return Math.round(num / 2);
    },
    getOverview(text){
      if(text.length > 200) return text.slice(0,200) + '...';
      return text
    }
  },
}
</script>

<style lang="scss" scoped>
.card {
  position: relative;
  height: 500px;
  box-shadow: 0 0 40px 2px rgba(0, 0, 0, 0.436);


  &:hover .caption {
    display: block;
  }

  >img {
    display: block;
    height: 100%;

  }

  .caption {
    position: absolute;
    top: 0;
    left: 0;
    display: none;
    width: 100%;
    height: 100%;
    color: white;
    background-color: rgba(0, 0, 0, 0.452);
    .caption-wrap {
      padding: 2rem;

      h3,
      h5{
        margin-bottom: .75rem;
      }

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

      .overview {
        padding: 2rem 0;
        overflow: hidden;
      }
    }
  }
}
</style>