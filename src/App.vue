<template>
  <AppHeader @search="getSearch" />
  <AppMain 
  :films="filmList"/>
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
      accessToken: 'eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJlNGM5MmM0NzNiYmI1NmI3ZDhjMmVjM2EyNzkwYTA4MCIsInN1YiI6IjY1ODJjODA4ZjE3NTljNDEyYjEwYTVkMiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.j1wZCyGLSuFiO4DMNMVrnnTVg229tm3I2PkaHYYNfZI',
      filmList: []
    }
  },
  methods: {
    getSearch(text) {
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          query: text,
          language: 'it-IT',
          includes_adult: true,
          page: 1
        },
        headers: {
          Authorization: `Bearer ${this.accessToken}`,
        }
      })
        .then((response) => {
          console.log(response);
          this.filmList = response.data.results;
          console.log(this.filmList);                    
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
