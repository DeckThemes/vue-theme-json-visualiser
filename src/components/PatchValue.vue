<template>
    <div class="card mb-2">
        <div class=" card-header">
            <div class="input-group input-group-sm">
                <label class="input-group-text" :for="id+1">Option Name</label>
                <input class="form-control" type="text" :id="id+1" :disabled="disabled" v-model="modelValue.patchOptionName"/>
                <label class="input-group-text"  :for="id+2">Default?</label>
                <div class="input-group-text">
                    <input class="form-check-input" type="checkbox" :id="id+2" v-model="modelValue.default" />
                </div>
            </div>
        </div> 
        <div class="card-body">
            <Injects class="injects mb-3" v-model="modelValue.injects" />
            <Components class="injects" v-model="modelValue.components" />
        </div> 
   </div>
</template>

<script setup>
import { reactive, ref } from 'vue';
import Injects from "./Injects.vue"
import Components from "./Components.vue"

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
            ]),
            components: reactive([])
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

.input-group {
    width: 70%;
    margin: auto;
    min-width: 400px;
}
</style>