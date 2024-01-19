<script setup lang="ts">
import {EditorState} from "prosemirror-state";
import {EditorView} from "prosemirror-view";
import {Schema} from "prosemirror-model";
import {schema} from "prosemirror-schema-basic";
import {addListNodes} from "prosemirror-schema-list";
import {exampleSetup} from "prosemirror-example-setup";
import {onMounted} from "vue";

const mySchema = new Schema({
  nodes: addListNodes(schema.spec.nodes, "paragraph block*", "block"),
  marks: schema.spec.marks
})

onMounted(() => {
  new EditorView(document.querySelector("#editor"), {
    state: EditorState.create({
      schema: mySchema,
      plugins: exampleSetup({schema: mySchema})
    })
  })
})
</script>

<template>
  <div id="editor"></div>
</template>