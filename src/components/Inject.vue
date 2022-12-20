<template>
    <section class="inject">
        <input type="text" v-model="filename"/>
        <div v-for="x in a">
            <input type="checkbox" :name="x" @change="check($event)" />
            <label :for="x">{{x}}</label>
        </div>
    </section>
</template>

<script setup>
import {reactive, ref} from "vue"

const props = defineProps({
    initialFilename: String
})

const filename = ref(props.initialFilename);
const a = reactive(["SP", "MainMenu", "QuickAccess"])
const checked = reactive([])

function check(e) {
    if (e.target.checked){
        this.checked.push(e.target.name)
    }
    else {
        var index = this.checked.indexOf(e.target.name);
        if (index !== -1) {
            this.checked.splice(index, 1);
        }
    }
    console.log(e)
    console.log(this.checked)
    console.log(filename.value)
}
</script>