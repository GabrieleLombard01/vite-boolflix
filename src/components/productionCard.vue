<script >
import { pics } from '../data';
export default {
    props: {
        item: Object
    },
    computed: {
        title() {
            return this.item.title || this.item.name
        },
        originalTitle() {
            return this.item.original_title || this.item.original_name
        },
        hasFlag() {
            const availableFlags = ['it', 'en'];
            return availableFlags.includes(this.item.original_language);
        },
        flagSrc() {
            const url = new URL(`../assets/img/${this.item.original_language}.png`, import.meta.url);
            return url.href
        },
        posterPath() {
            if (!this.item.poster_path) return pics.placeholder;
            return pics.prefix + this.item.poster_path;
        },
        vote() {
            return Math.ceil(this.item.vote_average / 2)
        }
    }
};
</script>

<template>
    <ul class="bg-black card_container">
        <div class="card_hover">
            <li>
                <h4 class="d-inline pe-2">Titolo:</h4>{{ title }}
            </li>
            <li>
                <h4 class="d-inline pe-2">Titolo originale:</h4>{{ originalTitle }}
            </li>
            <li>
                <h4 class="d-inline pe-2">Lingua originale:</h4>
                <img class="flag_size" v-if="hasFlag" :src="flagSrc" :alt="item.original_language">
                <span v-else>{{ item.original_language }}</span>
            </li>
            <li>
                <h4 class="d-inline pe-2">Voto:</h4>
                <i v-for="n in 5" :key="n" :class="n <= vote ? 'fa-solid' : 'fa-regular'" class="fa-star"></i>
            </li>
        </div>

        <li><img class="position-relative poster" :src="posterPath" :alt="title"></li>
    </ul>
</template>

<style scoped>
/*CSS reset*/
/*Pseudo-classes*/
.card_container:hover .card_hover {
    display: block;
    cursor: pointer;
}

/*Generics*/
/*Utilties*/


/*CARD:*/
.card_hover {
    width: 310px;
    height: 450px;
    color: white;
    background-color: rgba(0, 0, 0, 0.8);
    padding: 50px 15px 10px 15px;
    line-height: 40px;
    position: absolute;
    z-index: 1;
    display: none;
}
</style>