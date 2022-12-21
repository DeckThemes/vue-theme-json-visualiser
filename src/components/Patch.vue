<template>
    <section class="patchValues">
        <div>
            <label v-if="disableNameInput == false" :for="id+1">Patch Name:</label>
            <input type="text" :id="id+1" v-model="modelValue.patchName" :disabled="disableNameInput==true" />
        </div>
        <div v-if="hideTypeSelect==false">
            <label v-if="disableNameInput == false" :for="id+2">Patch Type:</label>
            <select :id="id+2" v-model="modelValue.type" @change="onTypeChange()">
                <option v-for="x in types" :value="x">{{ x }}</option>
            </select>
        </div>
        <PatchValues :disabled="disabled" v-model="modelValue.values" />
    </section>
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

        disabled.value = true
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

        disabled.value = true
    }
}
</script>