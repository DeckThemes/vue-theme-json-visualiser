<template>
    <section class="components">
        <Component v-for="(x,i) in modelValue" v-model="modelValue[i]" />
        <button class="btn btn-outline-primary btn-sm" @click="add()">Add Component</button> 
        <button class="btn btn-outline-secondary btn-sm" @click="remove()" :disabled="modelValue.length <= 0">Remove Last Component</button> 
    </section>
</template>

<script setup>
import { reactive, ref } from 'vue';
import Component from "./Component.vue"

const props = defineProps({
    modelValue: {
        type: Array,
        default: reactive([])
    },
    disabled: {
        type: Boolean,
        default: false,
    }
})

function add(){
    props.modelValue.push(reactive({
        componentName: "New Component",
        type: "image-picker",
        default: "",
        cssVariable: "my-cool-component-css-variable",
        tabs: []
    }))
    console.log(props.modelValue)
}

function remove(){
    props.modelValue.pop()
}

</script>

<style scoped>
.btn-outline-primary {
    margin-right: 5px;
}
</style>