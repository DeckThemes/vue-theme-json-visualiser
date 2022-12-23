<template>
    <div class="card">
        <div class="card-header">
            <div class="input-group input-group-sm patchName">
                <label v-if="disableNameInput == false" class="input-group-text" :for="id+1">Patch Name</label>
                <input class="form-control" type="text" :id="id+1" v-model="modelValue.patchName" :disabled="disableNameInput==true" />
                <label v-if="disableNameInput == false && hideTypeSelect == false" :for="id+2" class="input-group-text">Type</label>
                <select class="form-select" :id="id+2" v-model="modelValue.type" @change="onTypeChange()" v-if="hideTypeSelect==false">
                    <option v-for="x in types" :value="x">{{ x.charAt(0).toUpperCase() + x.slice(1) }}</option>
                </select>
            </div>
        </div>
        <div class="card-body">
            <PatchValues :disabled="disabled" v-model="modelValue.values" />
        </div>
    </div>
</template>

<script setup>
import { reactive, ref } from 'vue';
import PatchValues from "./PatchValues.vue"

const id = String(Math.random());

const props = defineProps({
    modelValue: {
        type: Object,
        default: {
            values: reactive([{
                patchOptionName: "Test",
                default: ref(false),
                injects: reactive([
                    {
                        filename: "1",
                        tabs: ["SP"]
                    }
                ])
            }]),
            patchName: "New Patch",
            type: "dropdown",
        }
    },
    disableNameInput: Boolean,
    hideTypeSelect: Boolean,
})

const disabled = ref(false)
const types = ["dropdown", "slider", "checkbox", "none"]

function setDisabledState(type){
    disabled.value = type === "checkbox" || type === "none"
}

function onTypeChange() {
    let type = this.props.modelValue.type
    console.log(type)

    disabled.value = false

    if (type === "checkbox") {
        this.props.modelValue.values.length = 0;
        this.props.modelValue.values.push(reactive({
            patchOptionName: "Yes",
            default: ref(false),
            injects: reactive([]),
            components: reactive([])
        }))
        this.props.modelValue.values.push(reactive({
            patchOptionName: "No",
            default: ref(true),
            injects: reactive([]),
            components: reactive([])
        }))
    }

    if (type === "none") {
        this.props.modelValue.values.length = 0;
        this.props.modelValue.values.push(reactive(
            {
                patchOptionName: "Inject",
                default: ref(true),
                injects: reactive([]),
                components: reactive([])
            }
        ))
    }

    setDisabledState(this.props.modelValue.type)
}

setDisabledState(props.modelValue.type)
</script>

<style scoped>
.patchName {
    width: 70%;
    margin: auto;
    min-width: 400px;
}

.headerThingy {
    margin: auto 7px;
}
</style>