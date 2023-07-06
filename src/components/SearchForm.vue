<script>
export default {
    data() {
        return {
            searchTerm: ''
        }
    },
    props: {
        placeholder: String,
        submitLabel: String,
    },
    emits: ['term-change', 'form-submit']
};
</script>

<template>
    <form @submit.prevent="$emit('form-submit')">
        <input v-model.trim="searchTerm" :placeholder="placeholder || 'Cerca...'" type="text"
            @keyup="$emit('term-change', searchTerm)">
        <button type="submit">{{ submitLabel || 'VAI' }}</button>
    </form>
</template>

