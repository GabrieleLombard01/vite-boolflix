<script>
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
            console.log(this.titleFilter)
        }
    }
};
</script>

<template>
    <SearchForm @term-change="setTitleFilter" @form-submit="searchMovie" />
</template>

<style></style>
