<template>
    <section class="injectswrapper">
        <section class="injects">
            <Inject v-for="(x, i) in injects" v-model="injects[i]" />
        </section>
        <button @click="add()">+</button> 
        <button @click="remove()">-</button> 
    </section>
</template>

<script setup>
import {reactive, ref} from "vue"
import Inject from "./Inject.vue"

const injects = reactive([
    {
        filename: "1",
        tabs: ["SP"]
    },
    {
        filename: "2",
        tabs: ["QuickAccess"]
    }
])

function add(){
    injects.push({filename: "Shared.css", tabs: ["SP"]})
}

function remove(){
    injects.pop()
}
</script>