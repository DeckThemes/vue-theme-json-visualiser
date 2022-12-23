<template>
    <section class="injectswrapper">
        <section class="injects">
            <Inject v-for="(x, i) in modelValue" v-model="modelValue[i]" />
        </section>
        <button @click="add()" class="btn btn-outline-primary btn-sm">Add File</button> 
        <button @click="remove()" :disabled="modelValue.length <= 0" class="btn btn-outline-secondary ml-5 btn-sm">Remove Last File</button> 
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

<style scoped>
.ml-5 {
    margin-left: 5px;
}
</style>