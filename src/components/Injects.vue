<template>
    <section class="injectswrapper">
        <section class="injects">
            <Inject v-for="(x, i) in modelValue" v-model="modelValue[i]" />
        </section>
        <button @click="add()">+</button> 
        <button @click="remove()">-</button> 
    </section>
</template>

<script setup>
import {reactive, ref} from "vue"
import Inject from "./Inject.vue"

const props = defineProps({
    modelValue: {
        type: Array,
        default: reactive([
            {
                filename: "1",
                tabs: ["SP"]
            },
            {
                filename: "2",
                tabs: ["QuickAccess"]
            }
        ])
    }
})

function add(){
    this.props.modelValue.push(reactive({filename: "Shared.css", tabs: ["SP"]}))
    console.log(this.props.modelValue)
}

function remove(){
    this.props.modelValue.pop()
}
</script>