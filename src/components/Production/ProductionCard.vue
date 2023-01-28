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
        },
        halfStars() {
            return Math.ceil(this.item.vote_average / 2);
        }
    }
};
</script>

<template>
    <div class="production-card text-center text-dark pointer border p-0 mx-1">
        <img class="img-fluid h-100 w-100 cover" :src="pathSrc" :alt="title">
        <div class="text p-1  h-100 text-light d-flex flex-column justify-content-between">
            <h3 class="fw-bolder">Titolo: {{ title }}</h3>
            <h4> Titolo originale: {{ originalTitle }}</h4>
            <p v-show="item.overview" class="fs-5">Descrizione: {{ item.overview }}</p>
            <div>
                <img class="img-fluid w-25" v-if="hasFlag" :src="flagSrc" :alt="item.original_language">
                <h3 v-else>{{ item.original_language }}</h3>
            </div>
            <div>
                <font-awesome-icon v-for="star in halfStars" icon="fa-solid fa-star" class="red"></font-awesome-icon>
                <font-awesome-icon v-for="star in 5 - halfStars" icon="fa-solid fa-star"
                    class="light"></font-awesome-icon>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.production-card {
    position: relative;
    flex-basis: calc(25% - 0.5rem);

    .cover {
        transition: opacity 1s ease-in-out;
    }

    .text {
        visibility: hidden;
        opacity: 0;
        transition: visibility 0s, opacity 1s ease-in-out;
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        background-color: black;
        overflow-y: auto;
    }
}



.production-card:hover {
    .cover {
        opacity: 0;
    }

    .text {
        visibility: visible;
        opacity: 1;
        transition: opacity 1s ease-in-out;
    }
}


.light {
    color: grey;
}

.red {
    color: red;
}
</style>