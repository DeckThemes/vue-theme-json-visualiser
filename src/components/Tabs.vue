<template>
    <section>
        <div v-for="x in tabs" class="tab">
            <input class="checkbox" type="checkbox" :id="x+id" :checked="modelValue.indexOf(x) >= 0" @change="check($event, x); $emit(`compute`)" />
            <label :for="x+id">{{x}}</label>
        </div>
    </section>
</template>

<script setup>
const tabs = ["SP", "MainMenu", "QuickAccess", "SteamLibraryWindow|Steam"]
const id = String(Math.random());

const props = defineProps({
    modelValue: Array
})

function check(e, tab) {
    if (e.target.checked){
        props.modelValue.push(tab)
    }
    else {
        var index = props.modelValue.indexOf(tab);
        if (index !== -1) {
            props.modelValue.splice(index, 1);
        }
    }
    console.log(props.modelValue)
}
</script>

<style scoped>
.checkbox {
    display: none;
}

.checkbox+label {
    color: #000;
    padding: 0px 5px;
}

.checkbox:checked+label {
    color: #fff;
    background-color: #000;
    border-radius: 5px;
}

.tab {
    margin-left: 2px;
    display: flex;
}

section {
    display: flex;
    flex-flow: row wrap;
}
</style>