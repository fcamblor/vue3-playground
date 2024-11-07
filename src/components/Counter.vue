<template>
  <button type="button" @click="count++">count is {{ count }}</button>
</template>

<script setup lang="ts">
import {ref} from "vue";

const props = defineProps({
  initialValue: Number
})
const count = ref(props.initialValue)
</script>

<style scoped>

</style>
