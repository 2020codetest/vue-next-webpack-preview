<template>
    <div>
        <span>当前时间：{{count}}</span>
        <br/>
        <span>外部变量：{{name}}</span>
        <br/>
        <button @click="emitEvent">传递事件</button>
    </div>
</template>

<script lang="ts">
import { ref, Ref, Prop, onMounted, defineComponent, SetupContext } from 'vue'
export default {
    props: {
        name: String
    },
    setup: (props: any, context: SetupContext) => {
        console.log(props)
        console.log(context)
        onMounted(() => {
            console.log("子组件mounted")
        })

        const count: Ref<string> = ref(new Date().toString())
        const emitEvent: (...args: any[]) => void = (...args: any[]) => {
            console.log("子组件传递事件", args)
            context.emit("update", 132)
        }

        return {
            count,
            emitEvent
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
