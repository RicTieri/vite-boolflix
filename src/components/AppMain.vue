<template>
  <main>
    <div>
      <select name="genres" id="genres">
        <option v-for="genre in getMixedGenres()" value="">
          {{ genre.name }}
        </option>
      </select>
    </div>
    <section>
      <h2>Films</h2>
      <div class="section-wrapper">
        <CardMovie v-for="film in films" :film="film" @info_pop="openInfo(film)" />
      </div>
    </section>
    <section>
      <h2>Series TV</h2>
      <div class="section-wrapper">
        <CardSerie v-for="serie in series" :serie="serie" @info_pop="openInfo(serie)" />
      </div>
    </section>
    <CardInfo :id_cast="id_cast" :open="info" />
  </main>
</template>

<script>
import CardMovie from './CardMovie.vue';
import CardSerie from './CardSerie.vue';
import CardInfo from './CardInfo.vue';
import axios from 'axios';

export default {
  data() {
    return {
      info: false,
      apiUrl: 'e4c92c473bbb56b7d8c2ec3a2790a080',
      id_cast: [],
      movieGenres: [],
      serieGenres: [],
    };
  },
  created() {
    this.getGenres()
  },
  methods: {
    openInfo(choice) {
      this.info = true;
      axios.get(`https://api.themoviedb.org/3/movie/${choice.id}/credits`, {
        params: {
          api_key: this.apiUrl,
        }
      })
        .then((response) => {
          this.id_cast = response.data.cast.slice(0, 5);
        })
        .catch(function (error) {
          console.error(error);
        });
    },
    getGenres() {
      axios.get('https://api.themoviedb.org/3/genre/movie/list', {
        params: {
          api_key: this.apiUrl,
        }
      })
        .then((response) => {
          console.log(response);
          this.movieGenres = response.data.genres;
        })
        .catch(function (error) {
          console.error(error);
        });
      axios.get('https://api.themoviedb.org/3/genre/tv/list', {
        params: {
          api_key: this.apiUrl,
        }
      })
        .then((response) => {
          console.log(response);
          this.serieGenres = response.data.genres;
        })
        .catch(function (error) {
          console.error(error);
        });
    },
    getMixedGenres() {
      const allGenres = [...this.serieGenres, ...this.movieGenres];
      const uniqueGenres = allGenres.filter((genre, index, array) => {
        return index === array.findIndex(g => g.id === genre.id);
      });
      return uniqueGenres;
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
  },
  components: {
    CardMovie,
    CardSerie,
    CardInfo
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
  position: relative;

}

section {
  margin: 0 .5rem 3rem;
  padding: .5rem 1rem;
  border-radius: 10px;
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