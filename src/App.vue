<template>
  <AppHeader @search="getSearch" />
  <AppMain />
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
      apiUrl: 'https://api.themoviedb.org/3',
      apiKey: 'eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJlNGM5MmM0NzNiYmI1NmI3ZDhjMmVjM2EyNzkwYTA4MCIsInN1YiI6IjY1ODJjODA4ZjE3NTljNDEyYjEwYTVkMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.j1wZCyGLSuFiO4DMNMVrnnTVg229tm3I2PkaHYYNfZI',
      searchEndpoint: '/search/movie'
    }
  },
  methods: {
    getSearch(text) {
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          query: text,
        },
        headers: {
          Authorization: `Bearer ${this.apiKey}`,
        }
      })
        .then((response) => {
          console.log(response);
        })
        .catch(function (error) {
          console.error(error);
        });
    }

  },
  created() {
    this.getSearch()
  },
}
</script>

<style lang="scss">
@use './style/general.scss';
</style>
