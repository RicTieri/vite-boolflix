<template>
  <AppHeader @search="getSearch" />
  <AppMain 
  :films="filmList"
  :series="serieList"/>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import axios from 'axios';

export default {
  components: {
    AppHeader,
    AppMain
  },
  data() {
    return {
      apiUrl: 'e4c92c473bbb56b7d8c2ec3a2790a080',
      filmList: [],
      serieList: []
    }
  },
  methods: {
    getSearch(text){
      this.getFilm(text),
      this.getSeries(text)
    },
    getFilm(text) {
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: this.apiUrl,
          query: text,
          language: 'it-IT',
          includes_adult: true,
          page: 1
        }
      })
        .then((response) => {
          this.filmList = response.data.results;
        })
        .catch(function (error) {
          console.error(error);
        });
    },
    getSeries(text) {
      axios.get('https://api.themoviedb.org/3/search/tv', {
        params: {
          api_key: this.accessToken,
          query: text,
          language: 'it-IT',
          includes_adult: true,
          page: 1
        }
      })
        .then((response) => {
          this.serieList = response.data.results;
        })
        .catch(function (error) {
          console.error(error);
        });
    }

  },
  created() {
    this.getSearch('a')
  },
}
</script>

<style lang="scss">
@use './style/general.scss';
</style>
