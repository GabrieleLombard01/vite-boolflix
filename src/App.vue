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
            titleFilter: '',
            showMovieSection: false,
            showSeriesSection: false
        };
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
            };
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
            }

            this.fetchApi('search/movie', 'movies', 'showMovieSection');
            this.fetchApi('search/tv', 'series', 'showSeriesSection');
        },
        fetchApi(endpoint, target, section) {
            if (this[section]) {
                return; // Do nothing if the section is already visible
            }

            axios.get(`${api.baseUri}/${endpoint}`, this.axiosConfig)
                .then(res => {
                    store[target] = res.data.results;
                    this[section] = true;
                });
        }
    }
};
</script>

<template>
    <div class="container-xl bg-black text-white">
        <!-- HEADER -->
        <header class="d-flex align-items-center justify-content-between p-2 bg-black">
            <h1 class="col-6 text-danger">BOOLFLIX</h1>
            <SearchForm class="col-6 text-end" @term-change="setTitleFilter" @form-submit="searchProductions" />
        </header>

        <section id="movies">
            <h2 :class="{ 'd-block': showMovieSection, 'd-none': !showMovieSection }">Film:</h2>
            <productionCard v-for="movie in store.movies" :key="movie.id" :item="movie" />
        </section>

        <section id="series">
            <h2 :class="{ 'd-block': showSeriesSection, 'd-none': !showSeriesSection }">Serie tv:</h2>
            <productionCard v-for="serie in store.series" :key="serie.id" :item="serie" />
        </section>
    </div>
</template>
  
<style lang="scss">
@use '../src/assets/scss/style.scss';
</style>
  
  
