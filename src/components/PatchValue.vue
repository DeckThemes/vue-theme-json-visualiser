<template>
    <section class="patchValue">
        <input type="text" :disabled="disabled" v-model="modelValue.patchOptionName"/>
        <div>
            <input type="checkbox" :id="id" v-model="modelValue.default" />
            <label :for="id">Default</label>
        </div>
        <Injects class="injects" v-model="modelValue.injects" />
    </section>
</template>

<script setup>
import { reactive, ref } from 'vue';
import Injects from "./Injects.vue"

const id = String(Math.random());

const props = defineProps({
    modelValue: {
        type: Object,
        default: reactive({
            patchOptionName: "Test",
            default: ref(false),
            injects: reactive([
                {
                    filename: "1",
                    tabs: ["SP"]
                }
            ])
        })
    },
    disabled: {
        type: Boolean,
        default: false
    }
})
</script>

<style scoped> 
.injects {
    margin-left: 20px;
}
</style>