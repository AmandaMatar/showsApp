<script setup>
    import { defineProps,defineEmits } from 'vue';

    const emit = defineEmits(['selectShow'])

    const {isGameOfThrones} = defineProps([
        'isGameOfThrones'
    ])

    const emitSelectedShow = () => {
        emit("selectShow")
    }
</script>

<template>
    <div class="hero">
        <h1>{{ isGameOfThrones ? 'Game Of Thrones' : 'Rick and Morty'}}</h1>
        <p @click="emitSelectedShow">{{ isGameOfThrones ? 'Rick and Morty' : 'Game Of Thrones'}}</p>
    </div>
</template>

<style scoped>
.hero {
    height : 40vh;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    flex-direction: column
}
.hero img {
    position: absolute;
    height: 700px;
    opacity: 0.1;
}
.hero h1 {
    font-size: 100px;
    font-weight: bold;
}
.hero p {
    cursor: pointer;
}

</style>