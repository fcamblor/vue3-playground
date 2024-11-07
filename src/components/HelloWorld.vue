<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0);
(window as any).count = count;

const test = { value: 10 };
// try to edit window.test.value in console and see how this will not be reflected into the DOM
// ... until a new re-render is triggered (like, clicking on count button)
(window as any).test = test;

const arr = ref<string[]>([]);
(window as any).arr = arr;

const obj = ref<Record<string,string>>({});
(window as any).obj = obj;

const nestedObj = ref<{nested: Record<string,string>}>({nested:{}});
(window as any).nestedObj = nestedObj;


console.log(`in HelloWorld <script>`)
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    {{test.value}}
    {{arr.length}}
    {{Object.keys(obj).length}}
    {{Object.keys(nestedObj.nested).length}}
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
