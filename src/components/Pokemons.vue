<template>
  <div>
    <button @click="refreshPokemons()">Refresh Pokemons</button>
    <br/>
    Pokemons :
    <dl>
      <dt v-for="(pokemon, index) in pokemonsRef" :key="pokemon.id">
        <Pokemon :pokemon="pokemon" />
      </dt>
    </dl>
  </div>
</template>

<script setup lang="ts">

import {ref} from "vue";
import {fetchPokemons, Pokemon as PokemonType} from "../services/fetchPokemons.ts";
import Pokemon from "./Pokemon.vue";

const pokemonsRef = ref<PokemonType[]>([])
async function refreshPokemons() {
  pokemonsRef.value = await fetchPokemons();
}
</script>

<style scoped>

</style>
