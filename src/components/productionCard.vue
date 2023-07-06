<script >
export default {
    props: {
        item: Object
    },

}
</script>

<template>
    <ul>
        <li>{{ item.title || item.name }}</li>
        <li>{{ item.original_title || item.original_name }}</li>
        <li>{{ item.original_language }}</li>
        <li>{{ item.vote_average }}</li>
    </ul>
</template>

<style>
/*CSS reset*/

/*Pseudo-classes*/

/*Generics*/

/*Utilties*/
</style>