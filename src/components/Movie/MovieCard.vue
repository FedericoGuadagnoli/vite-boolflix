<script>
export default {
    name: 'MovieCard',
    props: {
        title: String,
        original_title: String,
        lang: String,
        vote: String
    }
}
</script>

<template>
    <div class="movie-card text-center p-2 text-dark">
        <h2>{{ title }}</h2>
        <h2>{{ original_title }}</h2>
        <h3>{{ lang }}</h3>
        <h3>{{ vote }}</h3>
    </div>
</template>

<style>

</style>