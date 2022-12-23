<template>
    <section class="patchValues">
        <PatchValue :disabled="disabled" v-for="(x,i) in modelValue" v-model="modelValue[i]" />
        <button class="btn btn-outline-primary btn-sm" :disabled="disabled" @click="add()">Add Patch Option</button> 
        <button class="btn btn-outline-secondary ml-5 btn-sm" :disabled="disabled || modelValue.length <= 0" @click="remove()">Remove Last Patch Option</button> 
    </section>
</template>

<script setup>
import { reactive, ref } from 'vue';
import PatchValue from "./PatchValue.vue"

const props = defineProps({
    modelValue: {
        type: Array,
        default: reactive([{
            patchOptionName: "Test",
            default: ref(false),
            injects: reactive([
                {
                    filename: "1",
                    tabs: ["SP"]
                }
            ])
        }])
    },
    disabled: {
        type: Boolean,
        default: false,
    }
})

function add(){
    props.modelValue.push(reactive({patchOptionName: "New Patch Option", injects: reactive([]), components: reactive([])}))
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