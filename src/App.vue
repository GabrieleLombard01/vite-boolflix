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
            axios.get(`${api.baseUri}/search/movie?api_key=${api.key}`)
                .then(res => {
                    store.movies = res.data.results;
                })
        }
    }
};
</script>

<template>
    <SearchForm @term-change="setTitleFilter" @form-submit="searchMovie" />
</template>

<style></style>
