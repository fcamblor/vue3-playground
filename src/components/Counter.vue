<template>
  <button type="button" @click="emits('on-increment-clicked', value || 42)">count is {{ value }}</button>
</template>

<script setup lang="ts">

const props = defineProps({
  value: Number
})
const emits = defineEmits<{
  (event: 'on-increment-clicked', currentValue: number): void
}>()
</script>

<style scoped>

</style>
