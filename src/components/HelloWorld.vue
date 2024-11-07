<script setup lang="ts">
import {computed, ref, watch} from 'vue'

defineProps<{ msg: string }>()

const emits = defineEmits<{
  (e: 'even-detected', count: number): void,
}>()


const count = ref(0);
(window as any).count = count;

const squarred = computed(() => {
  return count.value * count.value;
})

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

const btnRef = ref<HTMLButtonElement|undefined>(undefined);
watch([btnRef], ([btn]) => {
  console.log(`btn html: ${btn?.innerHTML}`);
})
watch([count], ([count]) => {
  if(count % 2 === 0) {
    emits('even-detected', count)
  }
})
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button ref="btnRef" type="button" @click="count++">count is {{ count }} => squarred: {{squarred}}</button>
    {{test.value}}
    {{arr.length}}
    {{Object.keys(obj).length}}
    {{Object.keys(nestedObj.nested).length}}
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
    <p>Count is {{count % 2===0?'even':'odd'}}</p>
    <p v-if="count % 2 === 0">EVEN !!</p>
    <ul>
      <li v-for="(val, index) in arr" :key="index">
        {{val}} <slot name="arr-value" :val="val" ></slot>
      </li>
    </ul>
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
