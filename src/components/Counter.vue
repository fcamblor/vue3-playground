<template>
    <button type="button" @click="emit('increment', value)">count is {{ value }}
      <slot :count="value" />
    </button>
</template>

<script setup lang="ts">

const props = defineProps({
  value: {
    required: true,
    type: Number,
  }
})

const emit = defineEmits<{
  increment: [number]
  // (event: 'increment', currentCount: number): void;
}>()
</script>

<style scoped>

</style>
