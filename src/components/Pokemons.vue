<template>
  <div>
    <button @click="refreshPokemons()">Refresh Pokemons</button>
    <br/>
    Pokemons :
    <dl>
      <dt v-for="(pokemon, index) in pokemonsRef" :key="pokemon.id">
        <Pokemon :pokemon="pokemon"
                 @move-up="movePokemon(pokemon.id, (index+pokemonsRef.length-1)%pokemonsRef.length)"
                 @move-down="movePokemon(pokemon.id, (index+pokemonsRef.length+1)%pokemonsRef.length)"
        />
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

const movePokemon = (pokemonId: number, endingIndex: number) => {
  const startingIndex = pokemonsRef.value.findIndex(pk => pk.id === pokemonId)
  if(startingIndex !== -1) {
    const swap = pokemonsRef.value[endingIndex]
    pokemonsRef.value[endingIndex] = pokemonsRef.value[startingIndex]
    pokemonsRef.value[startingIndex] = swap;
  }
}
</script>

<style scoped>

</style>
