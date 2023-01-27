<script>
import SearchForm from './components/SearchForm.vue';
export default {
  components: { SearchForm },
  data() {
    return {
      filterMovie: ''
    }
  },
  methods: {
    OnTermChange(term) {
      this.filterMovie = term;
    }
  }
}
</script>

<template>
  <search-form @term-change="OnTermChange" placeholder="Scrivi il nome di un film"></search-form>
</template>

<style scoped lang="scss">
@use './assets/scss/style.scss' as *;
</style>
