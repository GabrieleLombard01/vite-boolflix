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
        <input v-model.trim="searchTerm" type="text" :placeholder="placeholder || 'Cerca...'"
            @keyup="$emit('term-change', searchTerm)">
        <button type="submit" @click="setSectionVisibility">{{ submitLabel || 'VAI' }}</button>
    </form>
</template>
  

  

