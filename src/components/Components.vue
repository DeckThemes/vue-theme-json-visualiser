<template>
    <section class="components">
        <Component v-for="(x,i) in modelValue" v-model="modelValue[i]" />
        <button @click="add()">+</button> 
        <button v-show="modelValue.length > 0" @click="remove()">-</button> 
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
    this.props.modelValue.push(reactive({
        componentName: "New Component",
        type: "image-picker",
        default: "",
        cssVariable: "my-cool-component-css-variable",
        tabs: []
    }))
    console.log(this.props.modelValue)
}

function remove(){
    this.props.modelValue.pop()
}

</script>