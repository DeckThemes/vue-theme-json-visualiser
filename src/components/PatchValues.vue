<template>
    <section class="patchValues">
        <PatchValue :disabled="disabled" v-for="(x,i) in modelValue" v-model="modelValue[i]" />
        <button :disabled="disabled" @click="add()">+</button> 
        <button :disabled="disabled" @click="remove()">-</button> 
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
    this.props.modelValue.push(reactive({patchOptionName: "New Patch Option", injects: reactive([]), components: reactive([])}))
    console.log(this.props.modelValue)
}

function remove(){
    this.props.modelValue.pop()
}

</script>

<style scoped>
.patchValues {
    margin-left: 20px;
}

</style>