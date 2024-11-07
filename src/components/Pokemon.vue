<template>
  <dt>{{pokemon.name}}</dt>
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
</script>

<style scoped>

</style>
