<script setup>
  import RickandMortyCards from "./components/RickandMortyCards.vue"
  import Hero from "./components/Hero.vue"
  import {ref} from "vue"
  import GameOfThronesCardsSuspense from "./components/GameOfThronesCardsSuspense.vue";

  const isGameOfThrones = ref(true)
</script>

<template>
  <main>
    <Hero 
      :isGameOfThrones="isGameOfThrones"
      @selectShow="isGameOfThrones = !isGameOfThrones"
    />
    <KeepAlive>
      <Component :is="isGameOfThrones ? GameOfThronesCardsSuspense : RickandMortyCards"/>
    </KeepAlive>
  </main>
</template>


