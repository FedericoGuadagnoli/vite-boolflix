<script>
import ProductionCard from './ProductionCard.vue';
import { store } from '../../data/store';
export default {
    name: 'ProductionList',
    data() {
        return {
            store
        }
    },
    components: { ProductionCard }
}
</script>

<template>
    <section id="movies" class="container my-5">
        <h1>MOVIES</h1>
        <div class="row g-4 row-cols-2 row-cols-md-3 row-cols-lg-4">
            <production-card v-for="movie in store.movies" :key="movie.id" :item="movie"></production-card>
        </div>
    </section>
    <section id="series" class="container my-5">
        <h1>SERIES</h1>
        <div class="row g-4 row-cols-2 row-cols-md-3 row-cols-lg-4">
            <production-card v-for="serie in store.series" :key="serie.id" :item="serie"></production-card>
        </div>
    </section>
</template>

<style>

</style>