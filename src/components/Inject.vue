<template>
    <section class="inject">
        <input type="text" v-model="modelValue.filename"/>
        <div v-for="x in tabs">
            <input class="checkbox" type="checkbox" :id="x+id" :checked="modelValue.tabs.indexOf(x) >= 0" @change="check($event, x)" />
            <label :for="x+id">{{x}}</label>
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
const id = String(Math.random());

function check(e, tab) {
    if (e.target.checked){
        this.props.modelValue.tabs.push(tab)
    }
    else {
        var index = this.props.modelValue.tabs.indexOf(tab);
        if (index !== -1) {
            this.props.modelValue.tabs.splice(index, 1);
        }
    }
    console.log(this.props.modelValue)
}
</script>

<style scoped>
.checkbox {
    display: none;
}

.checkbox+label {
    color: #ccc;
    padding: 0px 5px;
}

.checkbox:checked+label {
    color: #fff;
    background-color: #666;
    border-radius: 5px;
}

.inject {
    display: flex;
}

.inject > * {
    margin-right: 2px;
}
</style>