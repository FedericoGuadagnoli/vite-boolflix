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
    <section id="movies" class="container-fluid p-5">
        <h1 class="text-light">MOVIES</h1>
        <div class="row g-4 d-flex">
            <production-card v-for="movie in store.movies" :key="movie.id" :item="movie"></production-card>
        </div>
    </section>
    <section id="series" class="container-fluid p-5">
        <h1 class="text-light">SERIES</h1>
        <div class="row d-flex">
            <production-card v-for="serie in store.series" :key="serie.id" :item="serie"></production-card>
        </div>
    </section>
</template>

<style>

</style>