<template>
    <section class="inject">
        <div class="input-group input-group-sm mb-1">
            <label class="input-group-text" :for="id">File Name</label>
            <input class="form-control" type="text" :id="id" v-model="modelValue.filename" />
            <label class="input-group-text">Tabs</label>
            <Tabs v-model="modelValue.tabs" class="form-control" />
        </div>
    </section>
</template>

<script setup>
import Tabs from "./Tabs.vue"
const id = String(Math.random());

const props = defineProps({
    modelValue: {
        type: Object,
        default: {
            filename: "",
            tabs: []
        }
    }
})
</script>

<style scoped>
.inject {
    display: flex;
}

.inject > * {
    margin-right: 2px;
}
</style>