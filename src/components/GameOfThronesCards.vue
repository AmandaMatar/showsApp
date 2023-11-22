<!-- <script setup>
    import axios from "axios"
    import {ref, watch} from "vue"

    const characters = ref(null);
    const page = ref(0)
   
    const response = await axios.get("https://thronesapi.com/api/v2/Characters?limit=8");
    characters.value = response.data

    watch(page, async() => {
        const res = await axios.get(`https://thronesapi.com/api/v2/Characters?limit=8&offset=${page.value * 8}`);
        characters.value = res.data;
    })
</script>  -->

<script setup>
import { ref, computed } from "vue";
import axios from "axios";
import Card from "./Card.vue"
 
const characters = ref([]);
const currentPage = ref(1);
const charactersPerPage = 8;
 
const response = await axios.get("https://thronesapi.com/api/v2/characters");
characters.value = response.data;
 
const paginatedCharacters = computed(() => {
  const startIndex = (currentPage.value - 1) * charactersPerPage;
  const endIndex = startIndex + charactersPerPage;
  return characters.value.slice(startIndex, endIndex);
});
 
const nextPage = () => {
  if (
    currentPage.value < Math.ceil(characters.value.length / charactersPerPage)
  ) {
    currentPage.value++;
  }
};
 
const previousPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
};
</script>

<!-- <template>
    <div>
        <h1>Game Of Thrones Cards</h1>
        <h1>{{ characters }}</h1>
        <div>
            <button @click="page = page + 1">Next</button>
            <button @click="page = page - 1">Back</button>
        </div>
    </div>
</template> -->

<template>
    <div class="container">
        <div class="cards">
            <Card 
                v-for="character in characters"
                :key="character.id"
                :image="character.imageUrl"
                :fullName="character.fullName"
            >
                <div class="families">
                    <p>
                        {{ character.family }} 
                    </p>
                </div>
            </Card>
        </div>
        <div class="button-container">
            <button @click="page--">&lt</button>
            <button @click="page++">></button>
        </div>
    </div>
</template>

<style scoped>
.container {
    background-color: rgb(27, 26, 26);
    padding: 30px
}
.cards {
    max-width: 1000px;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
}
.cards h3 {
    font-weight: bold;
}
.cards p {
    font-size: 10px;
}
.button-container {
    display: flex;
    justify-content: center;
    padding-top: 30px
}
.button-container button {
    border: none;
    width: 50px;
    height: 50px;
    border-radius: 100%;
    margin: 0 5px;
    cursor: pointer;
}
.spinner {
    display: flex;
    align-items: center;
    justify-content: center;
}

p {
    font-size: 10px;
}

.families {
    display: flex;
    flex-wrap: wrap;
}

</style>