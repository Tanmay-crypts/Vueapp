<script setup>
import { ref, onMounted } from 'vue'
// reactive state
const count = ref(false)
// functions that mutate state and trigger updates
function increment() {
  count.value=true
}
const fncall=()=>{
  
}
// lifecycle hooks
onMounted(() => {
  console.log(`The initial count is ${count.value}.`)
})
</script>

<template>
<span class="head">
  <form action=""  @submit.prevent method="get">
    <input type="text" name="review" id="" placeholder="Enter your story">
    <button @click="increment">Submit</button>
    <input type="button" @click="increment" value="">
  </form>

</span>
<div>
  <h1 class="">by</h1>
</div>


</template>
<style scoped>
.head{
  position: fixed;
  top: 0;
  left: 50vw;
}
</style>