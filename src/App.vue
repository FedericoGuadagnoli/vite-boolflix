<script>
import axios from 'axios';
import SearchForm from './components/SearchForm.vue';
import MovieList from './components/Movie/MovieList.vue';
import { api } from './data';
import { store } from './data/store';
export default {
  name: 'Boolfix',
  components: { SearchForm, MovieList },
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
          const apiMovies = res.data.results;
          store.movies = apiMovies.map(movie => {
            const { title, original_title, original_language, vote_average } = movie;
            return { title, original_title, original_language, vote_average }
          })
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
  <movie-list></movie-list>
</template>

<style scoped lang="scss">
@use './assets/scss/style.scss' as *;
</style>
