<template>
  <dt>#{{pokemon.id}} {{pokemon.name}}
    <button @click="emit('move-up', pokemon)">⬆️</button>
    <button @click="emit('move-down', pokemon)">⬇️</button>
  </dt>
  <dd><img .src="pokemon.sprites.front_default || pokemon.sprites.back_default" /></dd>
</template>

<script setup lang="ts">
import {PropType} from "vue";
import {Pokemon} from "../services/fetchPokemons.ts";

defineProps({
  pokemon: {
    required: true,
    type: Object as PropType<Pokemon>
  }
})

const emit = defineEmits<{
  (event: 'move-up', pokemon: Pokemon): void,
  (event: 'move-down', pokemon: Pokemon): void,
}>()

</script>

<style scoped>

</style>
