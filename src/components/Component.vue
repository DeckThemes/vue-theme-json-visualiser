<template>
    <section class="component">
        <div>
            <label :for="id+1">Component Name:</label>
            <input type="text" :id="id+1" v-model="modelValue.componentName" />
        </div>
        <div>
            <label :for="id+2">Component Type:</label>
            <select :id="id+2" v-model="modelValue.type">
                <option v-for="x in types" :value="x">{{ x }}</option>
            </select>
        </div>
        <div>
            <label :for="id+3">Component Default value:</label>
            <input type="text" :id="id+3" v-model="modelValue.default" />
        </div>
        <div>
            <label :for="id+4">Component Css Variable Name:</label>
            <input type="text" :id="id+4" v-model="modelValue.cssVariable" />
        </div>
        <div>
            <label :for="id+5">Component Tabs:</label>
            <select :id="id+5" v-model="modelValue.tabs" multiple>
                <option v-for="x in tabs" :value="x">{{ x }}</option>
            </select>
        </div>
    </section>
</template>

<script setup>
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