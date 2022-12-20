<template>
    <section class="patches">
        <Patch v-for="(x,i) in modelValue" v-model="modelValue[i]" />
    </section>
    <button @click="add()">+</button> 
    <button @click="remove()">-</button> 
</template>

<script setup>
import { reactive, ref } from 'vue';
import Patch from "./Patch.vue"

const props = defineProps({
    modelValue: {
        type: Array,
        default: reactive([])
    }
})

function add(){
    this.props.modelValue.push(reactive({patchName: "New Patch", type: "dropdown",  values: reactive([])}))
    console.log(this.props.modelValue)
}

function remove(){
    this.props.modelValue.pop()
}

</script>

<style scoped>
.patches {
    margin-left: 20px;
}
</style>