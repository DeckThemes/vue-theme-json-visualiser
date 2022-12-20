<template>
    <section class="inject">
        <input type="text" v-model="modelValue.filename"/>
        <div v-for="x in tabs">
            <input type="checkbox" :name="x" :checked="modelValue.tabs.indexOf(x) >= 0" @change="check($event)" />
            <label :for="x">{{x}}</label>
        </div>
    </section>
</template>

<script setup>
const props = defineProps({
    modelValue: {
        type: Object,
        default: {
            filename: "",
            tabs: []
        }
    }
})

const tabs = ["SP", "MainMenu", "QuickAccess"]

function check(e) {
    if (e.target.checked){
        this.props.modelValue.tabs.push(e.target.name)
    }
    else {
        var index = this.props.modelValue.tabs.indexOf(e.target.name);
        if (index !== -1) {
            this.props.modelValue.tabs.splice(index, 1);
        }
    }
    console.log(this.props.modelValue)
}
</script>