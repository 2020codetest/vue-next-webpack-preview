<template>
    <div>
        <span>当前时间：{{count}}</span>
        <br/>
        <span>外部变量：{{name}}</span>
    </div>
</template>

<script lang="ts">
import { ref, Ref, Prop, onMounted, defineComponent } from 'vue'
export default {
    props: {
        name: String
    },
    setup: () => {
        onMounted(() => {
            console.log("子组件mounted")
        })

        const count: Ref<string> = ref(new Date().toString())
        return {
            count
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
