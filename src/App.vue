<script>
import axios from 'axios';
import { api } from './data';
import { store } from './data/store';
import SearchForm from './components/SearchForm.vue';
import productionCard from './components/productionCard.vue';
export default {
    components: { SearchForm, productionCard },
    data() {
        return {
            store,
            titleFilter: ''
        }
    },
    computed: {
        axiosConfig() {
            const { key, language } = api;

            return {
                params: {
                    language,
                    api_key: key,
                    query: this.titleFilter
                }
            }
        }
    },
    methods: {
        setTitleFilter(term) {
            this.titleFilter = term;
        },
        searchProductions() {
            if (!this.titleFilter) {
                store.movies = [];
                store.series = [];
                return;
            };

            this.fetchApi("search/movie", "movies");
            this.fetchApi("search/tv", "series");
        },

        fetchApi(endpoint, target) {
            axios.get(`${api.baseUri}/${endpoint}`, this.axiosConfig)
                .then(res => {
                    store[target] = res.data.results;
                });
        }
    }
};
</script>

<template>
    <SearchForm @term-change="setTitleFilter" @form-submit="searchProductions" />

    <section id="movies">
        <h2>Movies</h2>
        <productionCard v-for="movie in store.movies" :key="movie.id" :item="movie" />
    </section>

    <section id="series">
        <h2>Series</h2>
        <productionCard v-for="serie in store.series" :key="serie.id" :item="serie" />

    </section>
</template>

<style></style>
