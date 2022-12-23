<template>
    <div class="mb-1 component">
        <div class="input-group input-group-sm mb-1">
            <label class="input-group-text" :for="id+1">Component Name</label>
            <input class="form-control" type="text" :id="id+1" v-model="modelValue.componentName" />
        </div>
        <div class="input-group input-group-sm mb-1">
            <label class="input-group-text" :for="id+2">Component Type</label>
            <select class="form-select" :id="id+2" v-model="modelValue.type">
                <option v-for="x in types" :value="x">{{ x }}</option>
            </select>
        </div>
        <div class="input-group input-group-sm mb-1">
            <label class="input-group-text" :for="id+3">Component Default Value</label>
            <input class="form-control" type="text" :id="id+3" v-model="modelValue.default" />
        </div>
        <div class="input-group input-group-sm mb-1">
            <label class="input-group-text" :for="id+4">Component Css Variable Name</label>
            <input class="form-control" type="text" :id="id+4" v-model="modelValue.cssVariable" />
        </div>
        <div class="input-group input-group-sm">
            <label class="input-group-text">Component Tabs</label>
            <Tabs class="form-control" v-model="modelValue.tabs"/>
        </div>
    </div>  
</template>

<script setup>
import Tabs from "./Tabs.vue"
const props = defineProps({
    modelValue: {
        type: Object,
        default: {
            componentName: "New Component",
            type: "image-picker",
            default: "",
            cssVariable: "my-cool-component-css-variable",
            tabs: []
        }
    }
})

const id = String(Math.random());
const types = ["image-picker", "color-picker"]
const tabs = ["SP", "QuickAccess", "MainMenu"]
</script>

<style scoped>
.card-body {
    padding: 0;
}

.component:not(:first-child) {
    margin-top: 20px;
}

</style>