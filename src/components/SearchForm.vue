<script>
export default {
    props: {
        placeholder: String,
        submitLabel: String,
    }
};
</script>

<template>
    <form>
        <input :placeholder="placeholder || 'Cerca...'" type="text">
        <button>{{ submitLabel || 'VAI' }}</button>
    </form>
</template>

