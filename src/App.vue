<script>
import axios from 'axios';
import SearchForm from './components/SearchForm.vue';
import ProductionList from './components/Production/ProductionList.vue';
import { api } from './data';
import { store } from './data/store';
export default {
  name: 'Boolfix',
  components: { SearchForm, ProductionList },
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
    searchProduction() {
      if (!this.filterMovie) {
        store.movies = [];
        store.series = [];
        return;
      }
      this.fetchApi('search/movie', 'movies');
      this.fetchApi('search/tv', 'series');
    },
    fetchApi(endpoint, collection) {
      axios.get(`${api.baseUri}/${endpoint}`, this.axiosConfig)
        .then((res) => {
          store[collection] = res.data.results;
        });
    }
  }
};
</script>

<template>
  <search-form @term-change="onTermChange" @form-submit="searchProduction"
    placeholder="Scrivi il nome di un film"></search-form>
  <ProductionList></ProductionList>
</template>

<style scoped lang="scss">
@use './assets/scss/style.scss' as *;
</style>
