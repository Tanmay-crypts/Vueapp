<script setup>

import { ref, onMounted } from 'vue'
function handke(){
    return "hello"
}
// reactive state
const count = ref(0)

// functions that mutate state and trigger updates
function increment() {
  count.value++
}

// lifecycle hooks
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
  <button onclick=handke></button>
</template>