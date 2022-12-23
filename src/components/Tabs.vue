<template>
    <section>
        <div v-for="x in tabs" class="tab">
            <input class="checkbox" type="checkbox" :id="x+id" :checked="modelValue.indexOf(x) >= 0" @change="check($event, x)" />
            <label :for="x+id">{{x}}</label>
        </div>
    </section>
</template>

<script setup>
const tabs = ["SP", "MainMenu", "QuickAccess"]
const id = String(Math.random());

const props = defineProps({
    modelValue: Array
})

function check(e, tab) {
    if (e.target.checked){
        this.props.modelValue.push(tab)
    }
    else {
        var index = this.props.modelValue.indexOf(tab);
        if (index !== -1) {
            this.props.modelValue.splice(index, 1);
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