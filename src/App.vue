<script>
import axios from 'axios';
import SearchForm from './components/SearchForm.vue';
import { api } from './data';
import { store } from './data/store';
export default {
  name: 'Boolfix',
  components: { SearchForm },
  data() {
    return {
      filterMovie: '',
      store
    }
  },
  computed: {
    axiosConfig() {
      const { key, language } = api;
      return {
        params: {
          api_key: key,
          language: language,
          query: this.filterMovie
        }
      }
    },
  },
  methods: {
    onTermChange(term) {
      this.filterMovie = term;
    },
    searchMovies() {
      axios.get(`${api.baseUri}/search/movie`, this.axiosConfig)
        .then((res) => {
          store.movies = res.data.results
        }).catch((error) => {
          console.error(error)
        });
    }
  }
};
</script>

<template>
  <search-form @term-change="onTermChange" @form-submit="searchMovies"
    placeholder="Scrivi il nome di un film"></search-form>
</template>

<style scoped lang="scss">
@use './assets/scss/style.scss' as *;
</style>
