<template>
  <img src="./logo.png">
  <h1>Hello Vue 3!</h1>
  <button @click="inc">Clicked {{ count }} times.</button>
  <br/>
  <span>double count {{str}}</span>
  <br/>
  <span @click="updateProp">点击更新传递子组件的值: {{name}}</span>
  <br/>
  <br/>
  <br/>
  <div>子组件渲染如下</div>
  <TestComp ref="testRef" :name="name" v-on:update="childUpdate"></TestComp>
</template>

<script lang="ts">
import { ref, computed, Ref, ComputedRef, onMounted } from 'vue'
import { Convert } from "./Convert"
import TestComp from "./Comp/Test.vue"

export default {
  name: "App",
  components: {TestComp},
  setup: () => {    
    const testRef: any = ref(null)
    onMounted(() => {
        console.log("子组件实例", testRef.value)
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

    const updateProp: () => void = () => {
      name.value = "父组件传值 " + new Date().toString()
      testRef.value.subCompTestFunc()
    }

    return {
      count,
      inc,
      str,
      name,
      childUpdate,
      updateProp,
      testRef
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
