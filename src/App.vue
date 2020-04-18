<template>
  <img src="./logo.png">
  <h1>Hello Vue 3!</h1>
  <button @click="inc">Clicked {{ count }} times.</button>
  <span>double count {{str}}</span>
</template>

<script lang="ts">
import { ref, computed } from 'vue'
import { Convert } from "./Convert"

export default {
  setup() {
    const count = ref(0)
    const inc = () => {
      count.value++
    }

    const str = computed(() => Convert.ConvertToString(count.value))
    return {
      count,
      inc,
      str
    }
  }
}
</script>

<style scoped>
img {
  width: 200px;
}
h1 {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
