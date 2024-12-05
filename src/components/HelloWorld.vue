<script setup lang="ts">
import {computed, ref, toRef, toValue, watch} from 'vue'
import Counter from "./Counter.vue";
import LongLoadingComponent from "./LongLoadingComponent.vue";

defineProps<{ msg: string }>()
console.log('in HelloWorld')
const countRef = ref(0);
(window as any).count = countRef;

const squarred = computed(() => {
  const value = toValue(countRef);

  console.log('in squarred computing')
  return value * value;
})

const dateRef = ref(new Date())
setInterval(() => {
  dateRef.value = new Date()
}, 1000)

watch([countRef, dateRef], ([count, date]) => {
  console.log(`count/date updated: ${count} ${date.toISOString()}`)
}, {immediate: true})

function increment() {
  console.log('increment')
  countRef.value++;
}
function deferredIncrement() {
  setTimeout(() =>
    countRef.value += 1000,
    2000)
}
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <Counter @increment="increment()" :value="countRef">
      <template #blah="{ count }">
        <span style="color: red">Hello {{count}}</span>
      </template>
    </Counter>
    <Counter @increment="deferredIncrement()" :value="countRef" />
    <LongLoadingComponent />

    <ul>
      <li v-for="(value, index) in [1,2,3,4]" :key="value">{{value}}</li>
    </ul>


    {{ squarred }} | {{ dateRef.toISOString() }}
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Learn more about IDE Support for Vue in the
    <a
      href="https://vuejs.org/guide/scaling-up/tooling.html#ide-support"
      target="_blank"
      >Vue Docs Scaling up Guide</a
    >.
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
