<script>
export default {
    data() {
        return {
            searchTerm: '',
            sectionVisibilitySet: false
        };
    },
    props: {
        placeholder: String,
        submitLabel: String
    },
    emits: ['term-change', 'form-submit'],
    methods: {
        setSectionVisibility() {
            if (!this.sectionVisibilitySet) {
                this.$emit('form-submit');
                this.sectionVisibilitySet = true;
            }
        }
    }
};
</script>

<template>
    <form @submit.prevent="$emit('form-submit')">
        <button type="submit" @click="setSectionVisibility">{{ submitLabel }}<i
                class="fa-solid fa-magnifying-glass"></i></button>
        <input class="ps-2" v-model.trim="searchTerm" type="text" :placeholder="placeholder || 'Cerca...'"
            @keyup="$emit('term-change', searchTerm)">
    </form>
</template>
  
<style scoped>
/*CSS reset*/
/*Pseudo-classes*/
form input:focus {
    border: solid red 2px;
    width: 70%;
}

/*Generics*/
button {
    background-color: black;
    color: white;
    border-style: none;
    font-size: 30px;
    padding-right: 15px;
    position: relative;
    top: 3px;
}

form input {
    height: 35px;
    background-color: black;
    color: rgb(214, 213, 213);
    border: solid red 1px;
    border-radius: 3px;
}

/*Utilties*/
/*FORM:*/
</style>
  

