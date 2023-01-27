<script>
import { store } from '../../data/store';
export default {
    name: 'MovieList',
    data() {
        return {
            store
        }
    }
}
</script>

<template>
    <section id="movies" class="container my-5">
        <div class="row g-4 row-cols-2 row-cols-md-3 row-cols-lg-4">

        </div>
    </section>
</template>

<style>

</style>