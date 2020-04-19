<template>
    <div>
        <span @click="updateTime">点击更新当前时间：{{count}}</span>
        <br/>
        <span>compute 对象：{{compute}}</span>
        <br/>
        <span>外部变量：{{name}}</span>
        <br/>
        <button @click="emitEvent">传递事件</button>
    </div>
</template>

<script lang="ts">
import { ref, Ref, Prop, onMounted, defineComponent, SetupContext, watch, ComputedRef, computed } from 'vue'
export default {
    props: {
        name: String
    },
    setup: (props: Readonly<any>, context: SetupContext) => {
        console.log(props)
        console.log(context)
        onMounted(() => {
            console.log("子组件mounted")
        })

        const count: Ref<string> = ref(new Date().toString())
        watch(count, (val: string, old: string) => {
            console.log("count updated to be ", val)
        })

        const propRef: Ref<any> = ref(props)
        watch(propRef, (val: any, old: any) => {
            console.log("props updated to be ", propRef.value)
        }, {deep: true, immediate: true})

        const compute: ComputedRef<string> = computed<string>(() => {
            return "computed " + count.value;
        })

        watch(compute, (val: string, old: string) => {
            console.log("compute updated to be ", val)
        })

        const emitEvent: (...args: any[]) => void = (...args: any[]) => {
            console.log("子组件传递事件", args)
            context.emit("update", 132)
        }

        const updateTime: () => void = () => {
            count.value = new Date().toString()
        }

        return {
            count,
            emitEvent,
            updateTime,
            compute
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
