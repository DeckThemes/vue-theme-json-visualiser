<template>
    <section class="theme">
        <div>
            <label :for="id+1">Theme Name:</label>
            <input type="text" :id="id+1" v-model="modelValue.name" />
        </div>
        <div>
            <label :for="id+2">Theme Author:</label>
            <input type="text" :id="id+2" v-model="modelValue.author" />
        </div>
        <div>
            <label :for="id+3">Theme Target:</label>
            <select v-model="modelValue.target" :id="id+3">
                <option v-for="x in targets" :value="x">{{ x }}</option>
            </select>
        </div>
        <div>
            <label :for="id+4">Theme Version:</label>
            <input type="text" :id="id+4" v-model="modelValue.version" />
        </div>
        <div>
            <label :for="id+5">Theme Description:</label>
            <input type="text" :id="id+5" v-model="modelValue.description" />
        </div>
        <div>
            <Injects v-model="modelValue.injects" />
        </div>
        <div>
            <Patches v-model="modelValue.patches" />
        </div>
    </section>
</template>

<script setup>
import { reactive, ref } from 'vue';
import Injects from "./Injects.vue"
import Patches from "./Patches.vue"

const id = String(Math.random());
const targets = [
    "System-Wide",
    "Background",
    "Keyboard",
    "Home",
    "Background",
    "Library",
    "Store",
    "Friends and Chat",
    "Media",
    "Downloads",
    "Settings",
    "Lock Screen",
    "Tweak",
    "Other",
]
const props = defineProps({
    modelValue: Object
})
</script>