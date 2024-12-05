<template>
  <div>
    Hello ! This is a long loading component !
  </div>
</template>

<script setup lang="ts">
await new Promise(resolve => {
  setTimeout(resolve, 3000)
})
console.log(`component loading completed !`)
</script>

<style scoped>

</style>
