<template>
    <section class="inject">
        <div class="input-group input-group-sm mb-1">
            <button v-if="!isCssInject" class="btn btn-outline-secondary" type="button" id="button-addon1" @click="toCssInject()">Filename</button>
            <button v-if="isCssInject" class="btn btn-outline-secondary" type="button" id="button-addon1" @click="toFileInject()">Css Variable</button>
            <input class="form-control" type="text" :id="id" v-model="modelValue.filename" />
            <label v-if="isCssInject" class="input-group-text" :for="id+1">Value</label>
            <input v-if="isCssInject" class="form-control" type="text" :id="id+1" v-model="cssVarValue" @input="construct()" />
            <label class="input-group-text">Tabs</label>
            <Tabs v-model="tabs" class="form-control" @compute="construct" />
        </div>
    </section>
</template>

<script setup>
import { reactive, ref, computed } from 'vue';
import Tabs from "./Tabs.vue"
const id = String(Math.random());

const props = defineProps({
    modelValue: {
        type: Object,
        default: {
            filename: "",
            tabs: []
        }
    }
})

const isCssInject = ref(props.modelValue.filename.startsWith("--"))
const tabs = (isCssInject.value) ? reactive(props.modelValue.tabs.slice(1)) : reactive([...props.modelValue.tabs])
const cssVarValue = (isCssInject.value) ? ref(props.modelValue.tabs[0]) : ref("#FFFFFF")

function construct(){
    console.log("reconstructing")
    props.modelValue.tabs.length = 0
    if (isCssInject.value)
        props.modelValue.tabs.push(cssVarValue.value)
    props.modelValue.tabs.push(...tabs)
    console.log(props.modelValue.tabs)
}

function toCssInject(){
    isCssInject.value = true
    construct()
}

function toFileInject(){
    isCssInject.value = false
    construct()
}
</script>

<style scoped>
.inject {
    display: flex;
}

.inject > * {
    margin-right: 2px;
}
</style>