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

            this.fetchApi('search/movie', 'movies');
            this.fetchApi('search/tv', 'series');
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
    <div class="container-xl bg-black text-white">
        <!-- HEADER -->
        <header class="d-flex align-items-center justify-content-between p-2 bg-black">
            <h1 class="col-3">BOOLFLIX</h1>
            <SearchForm class="col-6 text-end" @term-change="setTitleFilter" @form-submit="searchProductions" />
        </header>

        <!-- SEARCHED PRODUCTS -->
        <section id="movies">
            <h2>Film:</h2>
            <div class="row justify-content-center">

                <productionCard class="card" v-for="movie in store.movies" :key="movie.id" :item="movie" />
            </div>
        </section>

        <section id="series">
            <h2>Serie tv:</h2>
            <div class="row">
                <productionCard class="card" v-for="serie in store.series" :key="serie.id" :item="serie" />

            </div>
        </section>
    </div>
</template>
  
<style lang="scss">
@use '../src/assets/scss/style.scss';

section {
    max-width: 992px;
    margin: 0 auto;
    padding-left: 10px;
}

.card {
    width: 310px;
    padding: 5px;
    margin: 10px;
}
</style>
  
  
  
  
  
