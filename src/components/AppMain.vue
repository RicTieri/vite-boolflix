<template>
  <main>
    <section class="navSection">
      <select name="genres" id="genres" v-model="selectedGenre" @change="searchByGender(selectedGenre)">
        <option value="">All Genres</option>
        <option v-for="genre in getMixedGenres()" :value="genre.id">
          {{ genre.name }}
        </option>
      </select>
    </section>
    <section>
      <h2>Films</h2>
      <div class="section-wrapper">
        <CardMovie v-for="film in filteredFilms" :film="film" @info_pop="openInfo(film)" />
        <p v-if="filteredFilms.length === 0">No results found for the selected genre.</p>
      </div>
    </section>
    <section>
      <h2>Series TV</h2>
      <div class="section-wrapper">
        <CardSerie v-for="serie in filteredSeries" :serie="serie" @info_pop="openInfo(serie)" />
        <p v-if="filteredSeries.length === 0">No results found for the selected genre.</p>
      </div>
    </section>
    <CardInfo :id_cast="infoCast" :open="info" :genres="infoGenre" />
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
      apiUrl: 'e4c92c473bbb56b7d8c2ec3a2790a080',
      movieGenres: [],
      serieGenres: [],
      selectedGenre: '',
      info: false,
      infoCast: [],
      infoGeneral: [],
      infoGenre: [],
    };
  },
  created() {
    this.getGenres();
    this.getMixedGenres()
  },
  methods: {
    openInfo(choice) {
      this.infoGenre = [];
      this.genreConvert(choice.genre_ids, this.getMixedGenres(), this.infoGenre);
      this.infoGeneral = choice;
      console.log(choice)
      this.info = true;
      axios.get(`https://api.themoviedb.org/3/movie/${choice.id}/credits`, {
        params: {
          api_key: this.apiUrl,
        }
      })
        .then((response) => {
          this.infoCast = response.data.cast.slice(0, 5);
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
      return uniqueGenres
    },
    genreConvert(choice, array, output) {
      choice.forEach((i) => {
        let match = array.find(g => g.id === i);
        output.push(match)
      })
    },
    searchByGender(selected) {
      this.selectedGenre = selected;
    }
  },
  computed: {
    filteredFilms() {
      if (!this.selectedGenre) {
        return this.films;
      } else {
        return this.films.filter(film => film.genre_ids.includes(parseInt(this.selectedGenre)));
      }
    },
    filteredSeries() {
      if (!this.selectedGenre) {
        return this.series;
      } else {
        return this.series.filter(serie => serie.genre_ids.includes(parseInt(this.selectedGenre)));
      }
    },
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

.navSection{
  text-align: right;
  margin-bottom: 1rem;
  select{
    background-color: rgba(0, 0, 0, 0.74);
    color: white;
    border-radius: 8px;
    padding: .25rem;
  }
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

    >p {
      color: white;
    }
  }
}
</style>