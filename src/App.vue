<script setup>
import { reactive, ref } from 'vue';

import Theme from "./components/Theme.vue"
const data = {
  manifest_version: 4,
  injects: {
    "shared.css": ["SP"]
  }
}

function setProperty(from, to, key, example){
    if (key in from)
        to[key] = from[key]
    else if (example)
        to[key] = example
}

function parseTheme(theme){
    if (theme.manifest_version !== 4)
        throw "Only manifest version 4 is supported"

    let res = {
        injects: [],
        patches: []
    }
    
    let common = {
        "name": "My Epic Theme",
        "author": "A Cool Person",
        "target": "Other",
        "version": "v1.2",
        "description": ""
    }

    
    for (const [key, value] of Object.entries(common))
        setProperty(theme, res, key, value)

    if ("injects" in theme)
        res.injects = parseInjects(theme.injects)

    if ("patches" in theme){
        for (const [key, value] of Object.entries(theme.patches))
            res.patches.push(parsePatch(key, value))
    }

    return res
}

function parsePatch(key, value){
    let components = ("components" in value) ? value.components : false
    let defaultValue = ("default" in value) ? value.default : false
    let values = []
    for (const [k, v] of Object.entries(value.values)){
        let c = []

        if (components){
            let i = components.find(x => x.on === k)
            if (i)
                c.push({
                    componentName: i.name,
                    type: i.type,
                    default: i.default,
                    css_variable: i.css_variable,
                    tabs: i.tabs
                })
        }

        values.push({
            patchOptionName: k,
            default: k === defaultValue,
            injects: parseInjects(v),
            components: c
        })
    }

    return {
        patchName: key,
        type: ("type" in value) ? value.type : "dropdown",
        values: values
    }
}

function parseInjects(injects){
    let items = []
    for (const [key, value] of Object.entries(injects)) {
        items.push({
            filename: key,
            tabs: value
        })
    }
    return items
}

function newFile(e){
  var file = e.target.files[0]; 
  var reader = new FileReader();
  reader.readAsText(file,'UTF-8');
  reader.onload = readerEvent => {
      var content = readerEvent.target.result; // this is the content!
      console.log( content );
      Object.assign(value, parseTheme(JSON.parse(content)))
   }
}

let value = reactive(parseTheme(data))
</script>

<template>
  <input type="file" @change="newFile($event)" />
  <Theme :model-value="value" />
</template>