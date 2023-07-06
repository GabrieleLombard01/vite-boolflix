<script>
import axios from 'axios';
import { api } from './data';
import { store } from './data/store';
import SearchForm from './components/SearchForm.vue';
export default {
    components: { SearchForm },
    data() {
        return {
            titleFilter: ''
        }
    },
    methods: {
        setTitleFilter(term) {
            this.titleFilter = term;
        },
        searchMovie() {
            if (!this.titleFilter) {
                store.movies = [];
                return;
            };

            const { key, language, baseUri } = api;

            const axiosConfig = {
                params: {
                    language,
                    api_key: key,
                    query: this.titleFilter
                }
            }

            axios.get(`${baseUri}/search/movie`, axiosConfig)
                .then(res => {
                    store.movies = res.data.results;
                });
        }
    }
};
</script>

<template>
    <SearchForm @term-change="setTitleFilter" @form-submit="searchMovie" />
    <section id="movies">
        <h2>Movies</h2>
        <ul v-for="movie in store.movies">
            <li>{{ movie.title }}</li>
            <li>{{ movie.original_title }}</li>
            <li>{{ movie.original_language }}</li>
            <li>{{ movie.vote_average }}</li>
        </ul>
    </section>
</template>

<style></style>
