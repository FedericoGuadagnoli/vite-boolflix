<script>
export default {
    name: 'ProductionCard',
    props: {
        item: Object
    },
    computed: {
        title() {
            return this.item.title || this.item.name;
        },
        originalTitle() {
            return this.item.original_title || this.item.original_name;
        },
        hasFlag() {
            const flags = ['it', 'en'];
            return flags.includes(this.item.original_language);
        },
        flagSrc() {
            const url = new URL(`../../assets/img/${this.item.original_language}.png`, import.meta.url);
            return url.href;
        },
        pathSrc() {
            const urlImage = `https://image.tmdb.org/t/p/w342${this.item.poster_path}`;
            return urlImage;
        }
    }
};
</script>

<template>
    <div class="production-card text-center p-2 text-dark">
        <img class="img-fluid" :src="pathSrc" :alt="title">
        <h2>{{ title }}</h2>
        <h2>{{ originalTitle }}</h2>
        <div>
            <img class="img-fluid" v-if="hasFlag" :src="flagSrc" :alt="item.original_language">
            <h3 v-else>{{ item.original_language }}</h3>
        </div>
        <h3>{{ item.vote_average }}</h3>
    </div>
</template>

<style>

</style>