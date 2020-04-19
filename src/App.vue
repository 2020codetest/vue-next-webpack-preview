<template>
  <img src="./logo.png">
  <h1>Hello Vue 3!</h1>
  <button @click="inc">Clicked {{ count }} times.</button>
  <span>double count {{str}}</span>
  <br/>
  <div>子组件渲染如下</div>
  <TestComp :name="name" v-on:update="childUpdate"></TestComp>
</template>

<script lang="ts">
import { ref, computed, Ref, ComputedRef, onMounted } from 'vue'
import { Convert } from "./Convert"
import TestComp from "./Comp/Test.vue"

export default {
  name: "App",
  components: {TestComp},
  setup: () => {    
    onMounted(() => {
        console.log("父组件mounted")
    })

    const count: Ref<number> = ref(0)
    const name: Ref<string> = ref("父组件传值")
    const inc: () => void = () => {
      count.value++
    }

    const str: ComputedRef<string> = computed(() => Convert.ConvertToString(count.value))
    const childUpdate: (val: number) => void = (val: number) => {
      console.log("收到子组件事件", val)
    }
    return {
      count,
      inc,
      str,
      name,
      childUpdate
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
