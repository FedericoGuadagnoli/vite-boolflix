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
    fetchApi(endpoint, collection,) {
      axios.get(`${api.baseUri}/${endpoint}?`, this.axiosConfig)
        .then((res) => {
          store[collection] = res.data.results;
        });
    }
  }
};
</script>

<template>
  <header>
    <div class="container-fluid px-5 h-100">
      <div class="row h-100">
        <div class="col-6 h-100 d-flex align-items-center">
          <h1 class="text-danger">BOOLFIX</h1>
        </div>
        <div class="col-6 d-flex align-items-center justify-content-end ">
          <search-form @term-change="onTermChange" @form-submit="searchProduction"
            placeholder="Scrivi il nome di un film"></search-form>
        </div>
      </div>
    </div>
  </header>
  <main>
    <ProductionList></ProductionList>
  </main>
</template>

<style lang="scss">
@use './assets/scss/style.scss' as *;
</style>
