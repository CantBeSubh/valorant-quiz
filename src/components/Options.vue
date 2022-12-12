<template>
    <div v-for="option in options" :key="option.id">
        <button @click="$emit('opt-click', option.correct)">{{ option.text }}</button>
    </div>
</template>

<script>
export default {
    name: "Options",
    props: {
        options: Array,
    },
    emits: ["opt-click"],
};
</script>
