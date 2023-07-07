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
        }
    }
};
</script>

<template>
    <ul>
        <li>{{ title }}</li>
        <li>{{ originalTitle }}</li>
        <li>
            <img class="flag_size" v-if="hasFlag" :src="flagSrc" :alt="item.original_language">
            <span v-else>{{ item.original_language }}</span>
        </li>
        <li>{{ item.vote_average }}</li>
        <li><img :src="posterPath" :alt="title"></li>
    </ul>
</template>

<style>
/*CSS reset*/

/*Pseudo-classes*/

/*Generics*/

/*Utilties*/
</style>