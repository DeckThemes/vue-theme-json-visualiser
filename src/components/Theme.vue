<template>
    <section class="theme">
        <div class="row">
            <div class="col-sm-6">
                <div class="card">
                    <div class="card-header">Theme Metadata</div>
                    <div class="card-body">
                        <div class="input-group input-group-sm mb-1">
                            <label class="input-group-text" :for="id+1">Name</label>
                            <input class="form-control" type="text" :id="id+1" v-model="modelValue.name" />
                        </div>
                        <div class="input-group input-group-sm mb-1">
                            <label class="input-group-text" :for="id+2">Author</label>
                            <input class="form-control" type="text" :id="id+2" v-model="modelValue.author" />
                        </div>
                        <div class="input-group input-group-sm mb-1">
                            <label class="input-group-text" :for="id+3">Target</label>
                            <select class="form-select" v-model="modelValue.target" :id="id+3">
                                <option v-for="x in targets" :value="x">{{ x }}</option>
                            </select>
                        </div>
                        <div class="input-group input-group-sm mb-1">
                            <label class="input-group-text" :for="id+4">Version</label>
                            <input class="form-control" type="text" :id="id+4" v-model="modelValue.version" />
                        </div>
                        <div class="input-group input-group-sm mb-1">
                            <label class="input-group-text" :for="id+5">Description</label>
                            <textarea rows="1" class="form-control" :id="id+5" v-model="modelValue.description" />
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-sm-6">
                <div class="card">
                    <div class="card-header">Always injected</div>
                    <div class="card-body">
                        <Injects v-model="modelValue.injects" />
                    </div>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <Patches v-model="modelValue.patches" />
            </div>
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

<style scoped>
.card {
    margin: 5px;
}

.card-header {
    text-align: center;
}

.row {
    width: 100%;
}
</style>