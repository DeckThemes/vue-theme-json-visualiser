<template>
    <div class="card">
        <div class="card-header">
            <span>Theme Patches</span>
            <button class="btn btn-outline-primary btn-sm" @click="add()">Add Patch</button> 
            <button class="btn btn-outline-secondary ml-5 btn-sm" @click="remove()" :disabled="modelValue.length <= 0">Remove Last Patch</button> 
        </div>
        <div class="card-body">
            <div class="row row-cols-1 row-cols-md-2 g-4">
                <div class="col" v-for="(x,i) in modelValue">
                    <Patch v-model="modelValue[i]" />
                </div>
            </div>
        </div>
    </div>

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
    props.modelValue.push(reactive({patchName: "New Patch", type: "dropdown",  values: reactive([])}))
    console.log(props.modelValue)
}

function remove(){
    props.modelValue.pop()
}

</script>

<style scoped>

.card-header {
    text-align: center;
}

.card-header > * {
    margin-right: 7px;
}
</style>