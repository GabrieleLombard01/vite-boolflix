<script>
import axios from 'axios';
import { api } from './data';
import { store } from './data/store';
import SearchForm from './components/SearchForm.vue';
export default {
    components: { SearchForm },
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

            axios.get(`${api.baseUri}/search/movie`, this.axiosConfig)
                .then(res => {
                    store.movies = res.data.results;
                });

            axios.get(`${api.baseUri}/search/tv`, this.axiosConfig)
                .then(res => {
                    store.series = res.data.results;
                });
        },

        fetchApi() {
            axios.get(`${api.baseUri}/search/tv`, this.axiosConfig)
                .then(res => {
                    store.series = res.data.results;
                });
        }
    }
};
</script>

<template>
    <SearchForm @term-change="setTitleFilter" @form-submit="searchProductions" />

    <section id="movies">
        <h2>Movies</h2>
        <ul v-for="movie in store.movies" :key="movie.id">
            <li>{{ movie.title }}</li>
            <li>{{ movie.original_title }}</li>
            <li>{{ movie.original_language }}</li>
            <li>{{ movie.vote_average }}</li>
        </ul>
    </section>

    <section id="series">
        <h2>Series</h2>
        <ul v-for="serie in store.series" :key="serie.id">
            <li>{{ serie.name }}</li>
            <li>{{ serie.original_name }}</li>
            <li>{{ serie.original_language }}</li>
            <li>{{ serie.vote_average }}</li>
        </ul>
    </section>
</template>

<style></style>
