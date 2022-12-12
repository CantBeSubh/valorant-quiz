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
<style scoped>
button {
    width: 100%;
    font-size: 16px;
    color: #ffffff;
    background-color: rgba(13, 0, 255, 0.3);
    border-radius: 15px;
    display: flex;
    padding: 10px;
    margin: 5px;
    justify-content: flex-start;
    align-items: center;
    border: 3px transparent none;
    cursor: pointer;
    transition: .4s;
}

button:hover {

    box-shadow: 0px 0px 200px rgba(13, 0, 255, 0.8);

}
</style>