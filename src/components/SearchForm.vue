<script>
export default {
    name: 'SearchForm',
    data() {
        return {
            term: ''
        }
    },
    props: {
        placeholder: String
    },
    emits: ['term-change', 'form-submit']
}
</script>

<template>
    <form class="d-flex gap-2" @submit.prevent="$emit('form-submit')">
        <input type="text" v-model.trim="term" class="form-control w-25" :placeholder="placeholder"
            @keyup="$emit('term-change', term)">
        <button class="btn btn-primary">Cerca</button>
    </form>
</template>

<style>

</style>