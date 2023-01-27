<script>
import MovieCard from './MovieCard.vue'
import { store } from '../../data/store';
export default {
    name: 'MovieList',
    data() {
        return {
            store
        }
    },
    components: { MovieCard }
}
</script>

<template>
    <section id="movies" class="container my-5">
        <div class="row g-4 row-cols-2 row-cols-md-3 row-cols-lg-4">
            <movie-card v-for="movie in store.movies" :key="movie.title" :title="movie.title"
                :original_title="movie.original_title" :lang="movie.original_language"
                :vote="movie.vote_average"></movie-card>
        </div>
    </section>
</template>

<style>

</style>